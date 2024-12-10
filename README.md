## Cruise Control for tubi

This is forked from https://github.com/linkedin/cruise-control

New features:
- Support amazon managed service for prometheus with sigv4 authentication


## How to build custom image for tubi

1. Clone repo: https://github.com/devops-ia/kafka-cruise-control
2. Update Dockerfile with the desired version of Cruise Control:
   ```
   ARG CC_TAG=renyu/sc-842448/feature/support-amazon-managed-service-for-prometheus
   
   RUN yum install -y wget git tar                                                                                           && \
    git clone -b ${CC_TAG} https://github.com/adRise/cruise-control.git                                           && \
    wget https://github.com/linkedin/cruise-control-ui/releases/download/v${CC_UI_TAG}/cruise-control-ui-${CC_UI_TAG}.tar.gz && \
    tar xzvf cruise-control-ui-${CC_UI_TAG}.tar.gz                                                                           && \
    mv cruise-control-ui cruise-control/                                                                                     && \
    rm -f cruise-control*.tar.gz
   ```
3. Build the image:
   ```
    docker buildx build --platform linux/amd64 -t 370025973162.dkr.ecr.us-east-2.amazonaws.com/cruise-control:jdk17-cc2.5.141-iam2.2-v1.0 .
    ```
4. Push the image to ECR:
   ```
   docker push 370025973162.dkr.ecr.us-east-2.amazonaws.com/cruise-control:jdk17-cc2.5.141-iam2.2-v1.0 
   ```