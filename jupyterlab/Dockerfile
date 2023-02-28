FROM python:3.8.16-bullseye # This version is compatible with Pycaret
#FROM python:3.11.2-buster
ARG DEBIAN_FRONTEND=noninteractive


# Adding packages and set time zone
RUN apt update && apt install -y \
    tzdata \
    build-essential \
    git \
    curl \
&&  ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
&&  apt clean \
&&  rm -rf /var/lib/apt/lists/*
ENV TZ=Asia/Tokyo


# Install nodejs
# https://github.com/nodesource/distributions
RUN curl -fsSL https://deb.nodesource.com/setup_19.x | bash - &&\
apt install -y nodejs


# Regarding Jupyterlab extensions
RUN python3 -m pip install --upgrade pip \
&&  pip3 install --no-cache-dir \
    black \
    jupyterlab \
    jupyterlab_code_formatter \
    jupyterlab-git \
    lckr-jupyterlab-variableinspector \
    jupyterlab_widgets \
    ipywidgets \
    import-ipynb \
    jupyter-resource-usage \
    jupyterlab-topbar \
    jupyterlab-topbar-text \
    jupyterlab-system-monitor \
    theme-darcula \
    jupyterlab_tabnine

# Default pip libraries you need
RUN pip3 install --no-cache-dir \
    numpy \
    pandas \
    scikit-learn \
    matplotlib \
    seaborn \
    plotly \
    requests \
    httpx \
    selectolax \
    bokeh \
    beautifulsoup4 \
    PyMySQL \
    SQLAlchemy \
    tqdm \
    tornado \
    Pillow \
    scipy \
    pycaret \
    sqlmodel


# Furthermore dependencies
COPY ./requirements.txt /requirements.txt
RUN pip3 install -r /requirements.txt



RUN jupyter labextension install \
    @jupyterlab/toc \
    && jupyter lab build -y \
    && jupyter lab clean -y