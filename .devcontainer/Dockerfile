FROM continuumio/miniconda3

# Install Apt packages and clean up
RUN apt-get update \
   && apt-get -y install --no-install-recommends tmux zsh htop \
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*

# Build Conda environment
RUN conda update --yes --all
ADD ./environment.yml /tmp/environment.yml
#RUN conda env update --file /tmp/environment.yml
RUN conda env create --file /tmp/environment.yml
# Install packages required by VSCode  
RUN conda install --name custom -y autopep8 pylint flake8
RUN conda clean --all

RUN apt update && apt install -y x11-apps