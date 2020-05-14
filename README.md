# Kustomize replace directive bug

Run `kustomize build overlay`.

Expected output:

```
      volumes:
      - name: certificates
        secret:
          items:
          - key: tls.key
            path: proxykey
          - key: tls.crt
            path: proxycert
          secretName: foo.cert
      - emptyDir: {}
        name: gunicorn-socket-dir
      - name: tls-dhparam-config
        secret:
          items:
          - key: dhparam
            path: dhparam
          secretName: skeleton-secrets
      - emptyDir: {}
        name: google-service-account
```

Actual output:

```
      volumes:
      - name: certificates
        secret:
          items:
          - key: tls.key
            path: proxykey
          - key: tls.crt
            path: proxycert
          secretName: foo.cert
      - name: tls-dhparam-config
        secret:
          items:
          - key: dhparam
            path: dhparam
          secretName: skeleton-secrets
```

Note that two of the volumes have been deleted erroneously.
