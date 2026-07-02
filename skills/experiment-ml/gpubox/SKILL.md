---
name: gpubox
description: Run or feasibility-check ML experiments on a personal idle GPU computer reached over SSH. Use when deciding whether a local/remote consumer GPU can run a training, evaluation, fine-tuning, or prototype job before launching it.
---

# gpubox - Personal Idle GPU Box

This skill is a template for using a spare personal computer as a small remote
GPU box for AI experiments. It is intentionally hardware-agnostic: the machine
could be a Windows laptop with WSL, a Linux desktop, or any always-on computer
reachable over SSH.

The main rule is simple: check feasibility before running anything. Consumer
GPUs are useful, but VRAM is usually the binding constraint.

## Suggested Setup

Create an SSH alias on the agent machine:

```sshconfig
Host gpubox
  HostName <tailscale-or-lan-hostname>
  Port 22
  User <remote-user>
  IdentityFile ~/.ssh/<your-gpubox-key>
  IdentitiesOnly yes
```

Recommended remote environment:

- NVIDIA GPU with working CUDA drivers.
- Python environment named `ml`, or another documented environment name.
- PyTorch installed with the matching CUDA build.
- `tmux` or `screen` for long-running jobs.
- Fast local disk for datasets and checkpoints.
- Optional private network such as Tailscale, ZeroTier, or a LAN-only SSH setup.

## Step 1 - Feasibility Gate

Before launching a job, collect hardware and environment facts:

```bash
ssh -o ConnectTimeout=12 gpubox 'nvidia-smi --query-gpu=name,memory.total,memory.free,memory.used,utilization.gpu --format=csv,noheader'
ssh gpubox 'python --version; which python; python - <<PY
import torch
print("torch", torch.__version__)
print("cuda", torch.cuda.is_available())
if torch.cuda.is_available():
    print(torch.cuda.get_device_name(0))
PY'
```

Then estimate:

- Model parameter count and dtype.
- Batch size, sequence length, image size, or sample length.
- Optimizer state memory.
- Activation memory.
- Dataset and checkpoint disk requirements.
- Expected runtime.

Give a clear verdict before running:

- `fits`: likely safe to run.
- `fits with changes`: reduce batch size, use LoRA/QLoRA, enable gradient
  checkpointing, shorten context, or use smaller inputs.
- `does not fit`: recommend CPU-only preprocessing, cloud GPU, or a smaller
  experiment.

## Step 2 - Run Pattern

Use the documented Python environment explicitly. Non-interactive SSH sessions
often do not source shell startup files.

Examples:

```bash
ssh gpubox 'conda run -n ml python train.py'
ssh gpubox 'conda run -n ml pip install <package>'
```

For longer runs:

```bash
ssh gpubox 'tmux new -d -s job "conda run -n ml python train.py 2>&1 | tee ~/job.log"'
ssh gpubox 'tail -n 40 ~/job.log; nvidia-smi --query-gpu=memory.used,utilization.gpu --format=csv,noheader'
```

## Step 3 - Practical Defaults

For small GPUs, prefer:

- LoRA or QLoRA instead of full fine-tuning.
- Small batch sizes with gradient accumulation.
- Mixed precision where stable.
- Gradient checkpointing when activation memory dominates.
- Small validation subsets before full evaluation.
- Checkpointing less often if disk is limited.

Do not leave long jobs running silently. Record the command, environment,
dataset, checkpoint, and result location so the experiment can be reproduced.

## Privacy Notes

Do not publish:

- Real SSH hostnames, private IP addresses, usernames, or ports.
- Private key filenames tied to a real machine.
- Tailscale node names.
- Absolute local paths that identify a person or workstation.

Keep public examples generic and ask users to fill in their own machine details.
