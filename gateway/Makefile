.DEFAULT_GOAL := all

# secrets:
# 	kubectl create secret generic gateway-tls --from-file=config/certs --dry-run -o yaml > k8s/gateway-tls.secret.yaml

configmap:
	kubectl create configmap gateway-config --from-file=config/ --dry-run -o yaml > k8s/gateway.configmap.yaml
	kubectl create configmap gateway-upstreams --from-file=config/upstreams --dry-run -o yaml > k8s/gateway-upstreams.configmap.yaml

clean:
	rm k8s/gateway.configmap.yaml k8s/gateway-upstreams.configmap.yaml k8s/gateway-tls.secret.yaml || true

all: clean | configmap # secrets
