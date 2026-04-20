Install OIDC Provider
'''
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster roboshop-1 \
    --approve
'''
create IAM Policy
'''
 curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v3.2.2/docs/install/iam_policy.json
'''   
 aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam-policy.json
'''  
create service account
'''
 eksctl create iamserviceaccount \
--cluster=roboshop-1 \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--attach-policy-arn=arn:aws:iam::593300579669:policy/AWSLoadBalancerControllerIAMPolicy \
--override-existing-serviceaccounts \
--region us-east-1 \
--approve 

'''

helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=roboshop-1 --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller