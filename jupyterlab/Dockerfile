FROM python:3.11.2-buster
ARG DEBIAN_FRONTEND=noninteractive


# Adding packages and set time zone
RUN apt update && apt install -y \
    tzdata \
    build-essential \
&&  ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
&&  apt clean \
&&  rm -rf /var/lib/apt/lists/*

ENV TZ=Asia/Tokyo


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
    import-ipynb


# Default pip libraries you need
RUN pip3 install --no-cache-dir \
    numpy \
    pandas \
    scikit-learn \
    matplotlib \
    seaborn \
    plotly \
    requests
#    scipy \
#    pycaret \
#    beautifulsoup4 \
#    Pillow \
#    bokeh \
#    widgetsnbextension

# Additional packages
#RUN pip install --no-cache-dir \
#    pydeps \
#    graphviz \
#    pandas_profiling \
#    shap \
#    umap \
#    xgboost \
#    lightgbm

# Furthermore dependencies
COPY ./requirements.txt /requirements.txt
RUN pip3 install -r /requirements.txt