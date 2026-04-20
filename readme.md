Install OIDC Provider
'''
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster roboshop-1 \
    --approve