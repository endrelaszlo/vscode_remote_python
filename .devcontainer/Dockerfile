FROM continuumio/miniconda3

# Install Apt packages and clean up
RUN apt-get update \
   && apt-get -y install --no-install-recommends tmux zsh htop x11-apps \
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
#RUN conda env update --file /tmp/environment.yml

# Create new environment
RUN conda env create --file /tmp/environment.yml

# Install packages required by VSCode  
RUN conda install --name custom -y autopep8 pylint flake8
RUN conda clean --all
