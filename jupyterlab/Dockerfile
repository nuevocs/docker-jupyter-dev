#FROM python:3.8.16-bullseye
FROM python:3.11.2-buster
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



# Install Java RE
RUN apt install -y openjdk-11-jre-headless


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
    theme-darcula
#    jupyterlab-topbar \
#    jupyterlab-topbar-text \
#    jupyterlab-system-monitor \
#    jupyterlab_tabnine

# Default pip libraries you need
RUN pip install --no-cache-dir \
    numpy \
    pandas \
    scikit-learn \
    scipy \
    matplotlib \
    seaborn \
    plotly \
    requests \
    httpx \
    selectolax \
    selenium \
    lxml \
    mitosheet \
    bokeh \
    beautifulsoup4 \
    PyMySQL \
    SQLAlchemy \
    tqdm \
    tornado \
    Pillow \
    sqlmodel \
    tabula-py
#    pycaret \

# install google chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
RUN apt-get -y update
RUN apt-get install -y google-chrome-stable

# install chromedriver
RUN apt-get install -yqq unzip
RUN wget -O /tmp/chromedriver.zip http://chromedriver.storage.googleapis.com/`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE`/chromedriver_linux64.zip
RUN unzip /tmp/chromedriver.zip chromedriver -d /usr/local/bin/


# Furthermore dependencies
COPY ./requirements.txt /requirements.txt
RUN pip install -r /requirements.txt



# Install Mitosheet to Jupyter \
RUN python -m jupyter nbextension install --py --user mitosheet
RUN python -m jupyter nbextension enable --py --user mitosheet


#RUN jupyter labextension install \
#    @jupyterlab/toc \
#    && jupyter lab build -y \
#    && jupyter lab clean -y
