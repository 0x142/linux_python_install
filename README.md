# linux_python_install

This guide describes how to install a particular version of python on linux from source  
Installing env  
And running the telegram bot as a service  

# Start

1. Install dependencies:

    ```bash
    sudo apt update && sudo apt upgrade -y
    sudo apt install -y build-essential libffi-dev libgdbm-dev libncursesw5-dev \
                        libreadline-dev libsqlite3-dev libssl-dev libbz2-dev \
                        liblzma-dev zlib1g-dev uuid-dev tk-dev curl
    ```

2. Download the required version of Python (3.12.2 in example):

    ```bash
    cd /usr/src
    sudo curl -O https://www.python.org/ftp/python/3.12.2/Python-3.12.2.tgz
    sudo tar -xf Python-3.12.2.tgz
    cd Python-3.12.2
    ```

3. Build and Install Python:

    ```bash
    sudo ./configure --enable-optimizations
    sudo make -j$(nproc)
    sudo make altinstall
    python3.12 --version
    ```

4. Create and activate a virtual environment with required version of Python:

    ```bash
    /usr/local/bin/python3.12 -m venv my_env
    source /my_env/bin/activate
    ```

5. Install requirments of your project:

    ```bash
    pip install --upgrade pip
    pip install -r requirements.txt
    ```

6. Add project and script `run_bot.sh` to my_env:

    ```bash
    /my_env/my_project/*
    chmod +x /my_env/my_project/run_bot.sh
    ```

7. Create systemd service `telegram_bot.service`:

    ```bash
    sudo nano /etc/systemd/system/tg_bot_service
    sudo systemctl daemon-reload
    sudo systemctl start telegram_bot.service
    sudo systemctl enable telegram_bot.service  
    ```
