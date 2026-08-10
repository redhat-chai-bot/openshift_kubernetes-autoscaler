FROM quay-proxy.ci.openshift.org/openshift/ci:openshift_release_golang-1.16 AS builder
WORKDIR /go/src/k8s.io/autoscaler
COPY . .
WORKDIR /go/src/k8s.io/autoscaler/cluster-autoscaler
RUN go build --tags openshift -o ./cluster-autoscaler .

FROM registry.access.redhat.com/ubi8/ubi-minimal
COPY --from=builder /go/src/k8s.io/autoscaler/cluster-autoscaler/cluster-autoscaler /usr/bin/
CMD /usr/bin/cluster-autoscaler
LABEL summary="Cluster Autoscaler for OpenShift and Kubernetes"
