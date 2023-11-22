# Istio-rate-limit
Implementing Rate Limit Using Istio

### How to Enable Global Rate Limit

1. Deploy Rate Limit Redis which will store rate limit configurations.
```sh
kubectl apply -f global-rate-limit/rate-limit-redis.yaml
```

2. Deploy Rate Limit Service which will handle rate limit logic.
```sh
kubectl apply -f global-rate-limit/rate-limit-service.yaml
```

3. Apply Envoy Filter which will add rate limit service as global rate limiter for istio.
```sh
kubectl apply -f global-rate-limit/envoyfilters/filter-ratelimit.yaml
```

4. Apply Envoy Filter which will get headers as descriptor that will be used for rate limit configuration.
```sh
kubectl apply -f global-rate-limit/envoyfilters/filter-ratelimit-svc.yaml
```

5. Apply Rate Limit Configuration as configmap that will be used by rate limit service.
```sh
kubectl apply -f global-rate-limit/rate-limit-config.yaml
```

## How to Enable Local Rate Limit

Apply Local Rate Limit using the below envoyfilter for service name `foo`
```sh
kubectl apply -f local-rate-limit/envoyfilter.yaml
```