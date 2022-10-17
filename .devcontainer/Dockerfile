FROM nvcr.io/nvidia/pytorch:22.09-py3
# FROM continuumio/miniconda3


# Install Apt packages and clean up
RUN apt-get update \
   && apt-get -y install --no-install-recommends tmux zsh htop x11-apps mesa-utils \
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*

# Might be needed later for OpenCV or Open3D
# RUN apt-get update
# RUN apt-get install ffmpeg libsm6 libxext6  -y
# RUN apt-get install libgl1  -y
# RUN apt-get install libgl1-mesa-glx  -y
# RUN apt-get install python3-opencv  -y

# Build Conda environment
RUN conda update --yes --all
ADD ./environment.yml /tmp/environment.yml

# Update the conda environment if the base environment has to be changed
RUN conda env update --file /tmp/environment.yml

# Create new environment
# RUN conda env create --file /tmp/environment.yml

# Install packages required by VSCode  
# RUN conda install --name custom -y autopep8 pylint flake8
RUN conda clean --all

# ZSH in Docker installer
# https://github.com/deluan/zsh-in-docker
# RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
# Uses "Spaceship" theme with some customization. Uses some bundled plugins and installs some more from github
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.3/zsh-in-docker.sh)" -- \
    -t https://github.com/denysdovhan/spaceship-prompt \
    -a 'SPACESHIP_PROMPT_ADD_NEWLINE="false"' \
    -a 'SPACESHIP_PROMPT_SEPARATE_LINE="false"' \
    -p git \
    -p ssh-agent \
    -p https://github.com/zsh-users/zsh-autosuggestions \
    -p https://github.com/zsh-users/zsh-completions
