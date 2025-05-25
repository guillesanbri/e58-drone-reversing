# e58-drone-reversing
Reverse-engineered video feed from an E58 drone.

# Setting Up

1. Install [uv](https://github.com/astral-sh/uv) if you don't have it:
```bash
curl -Ls https://astral.sh/uv/install.sh | sh
```

2. Clone the repo
```bash
git clone https://github.com/guillesanbri/e58-drone-reversing.git
cd e58-drone-reversing
```

3. Create the virtual environment and install dependencies:

```bash
uv venv
uv pip install .
```

4. Run the script:
```bash
uv run main.py
```
