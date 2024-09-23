# TrueCharts catalog
Copy of the main branch.
Feel free to create pull requests for version updates to the latest versions (like in the example)

The idea behind this branch is that you can keep using latest version of your favourite apps and updating them by only stopping them removing their respective images from **Manage Container Images
** and starting them again, this should redownload the newest version of the app and will work even if there is some internet outage and only restart the app (considering you have the image downloaded).

Note: with this it is small posibility that after some time some apps can break but this is very unlikely and would need the creator of the base app to change the run script for example adding required options etc. (this is based on that the TrueNAS will not break anything on their end)

## Original version (same as in the main branch)
```yaml
image:
  repository: esphome/esphome
  pullPolicy: IfNotPresent
  tag: 2024.5.4@sha256:29e21efe64d03646530025d056d545485ab9c40a35f3d99e8e0a90d79bde2356
securityContext:
  container:
    runAsNonRoot: false
    readOnlyRootFilesystem: false
    privileged: true
    allowPrivilegeEscalation: true
    runAsUser: 0
    runAsGroup: 0
service:
  main:
    ports:
      main:
        port: 6052
        targetPort: 6052
workload:
  main:
    podSpec:
      containers:
        main:
          probes:
            liveness:
              type: http
              path: /
            readiness:
              type: http
              path: /
            startup:
              type: http
              path: /
          env:
            ESPHOME_DASHBOARD_USE_PING: false
            ESPHOME_DASHBOARD_RELATIVE_URL: /
            # ESPHOME_QUICKWIZARD:
            # ESPHOME_IS_HASSIO:
            # DISABLE_HA_AUTHENTICATION:
            # USERNAME:
            # PASSWORD:
persistence:
  config:
    enabled: true
    mountPath: /config
  platformio:
    enabled: true
    mountPath: /.platformio
portal:
  open:
    enabled: true
```

## Updated version
```yaml
image:
  repository: esphome/esphome
  pullPolicy: IfNotPresent
  tag: latest
securityContext:
  container:
    runAsNonRoot: false
    readOnlyRootFilesystem: false
    privileged: true
    allowPrivilegeEscalation: true
    runAsUser: 0
    runAsGroup: 0
service:
  main:
    ports:
      main:
        port: 6052
        targetPort: 6052
workload:
  main:
    podSpec:
      containers:
        main:
          probes:
            liveness:
              type: http
              path: /
            readiness:
              type: http
              path: /
            startup:
              type: http
              path: /
          env:
            ESPHOME_DASHBOARD_USE_PING: false
            ESPHOME_DASHBOARD_RELATIVE_URL: /
            # ESPHOME_QUICKWIZARD:
            # ESPHOME_IS_HASSIO:
            # DISABLE_HA_AUTHENTICATION:
            # USERNAME:
            # PASSWORD:
persistence:
  config:
    enabled: true
    mountPath: /config
  platformio:
    enabled: true
    mountPath: /.platformio
portal:
  open:
    enabled: true
```

The difference is in the **image > tag**


