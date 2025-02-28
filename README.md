Having an override-able array like

`values1.yaml`:

```yaml
paths:
  values1-name-doesnt-matter:
    - path: "/path/from/values1"
      name: foo
```

`values2.yaml`:

```yaml
paths:
  # Disable defaults from HELM Chart, or previous valuesX.yaml
  #default:
  #values1-name-doesnt-matter:
  values2:
    - path: "/path/from/values2"
      name: bar

```

Render with

    helm template myrelease ./helm-override-array/ -f values1.yaml -f values2.yaml 

Expected Output:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  paths:
    - name: default1
      path: /default1
      claim: default1claim
    - name: default2
      path: /default2
      claim: default2
    - name: foo
      path: /path/from/values1
      claim: foo
    - name: bar
      path: /path/from/values2
      claim: bar
```
