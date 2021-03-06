# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM python:3.7.0-slim

RUN pip install mlflow

RUN apt-get update && apt-get -y install --no-install-recommends default-libmysqlclient-dev libpq-dev build-essential sqlite3 wget
    
RUN pip install mlflow==1.15.0 sqlalchemy==1.4.11 boto3==1.17.58

COPY start.sh /usr/local/bin

WORKDIR /usr/local/bin

RUN wget https://dl.min.io/client/mc/release/linux-amd64/mc && chmod +x mc

ENV MLFLOW_S3_ENDPOINT_URL http://10.96.0.4:9000
ENV AWS_ACCESS_KEY_ID submarine_minio
ENV AWS_SECRET_ACCESS_KEY submarine_minio
ENV BACKEND_URI sqlite:///store.db

EXPOSE 5000

CMD ./start.sh