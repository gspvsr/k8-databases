### Admin

1. Install EbS SCI Drivers.
---
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.28"
---
2. Provide access to Ec2 servers (it should be on role attached to EC2)
3. Create sc for EBS dynamic provisioning.
---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-sc
provisioner: ebs.csi.aws.com
volumeBindingMode: WaitForFirstConsumer
parameters:
  csi.storage.k8s.io/fstype: xfs
  type: io1
  iopsPerGB: "50"
  encrypted: "true"
---
4. aws eks update-kubeconfig --region us-east-1 --name eks-spot-cluster
----

install k9s :
curl -sS https://webi.sh/k9s | sh
