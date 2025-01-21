Install output

spec:
  replicas: 1
  revisionHistoryLimit: 3
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-server
      app.kubernetes.io/instance: argocd
  template:
    metadata:
      annotations:
        checksum/cmd-params: 319d56ae73721d7d7117931854629353486fc30e0448801c8d6337e46fe9aea0
        checksum/cm: 0c6acb003d37749ffaab2d73569f228c33c754ffd773e4cb885f35351713e5b9
      labels:
        helm.sh/chart: argo-cd-7.7.16
        app.kubernetes.io/name: argocd-server
        app.kubernetes.io/instance: argocd
        app.kubernetes.io/component: server
        app.kubernetes.io/managed-by: Helm
        app.kubernetes.io/part-of: argocd
        app.kubernetes.io/version: "v2.13.3"
    spec:
      terminationGracePeriodSeconds: 30
      serviceAccountName: argocd-server
      automountServiceAccountToken: true
      containers:
      - name: server
        image: quay.io/argoproj/argocd:v2.13.3
        imagePullPolicy: IfNotPresent
        args:
        - /usr/local/bin/argocd-server
        - --port=8080
        - --metrics-port=8083
        env:
          - name: ARGOCD_SERVER_NAME
            value: argocd-server
          - name: ARGOCD_SERVER_INSECURE
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.insecure
                optional: true
          - name: ARGOCD_SERVER_BASEHREF
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.basehref
                optional: true
          - name: ARGOCD_SERVER_ROOTPATH
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.rootpath
                optional: true
          - name: ARGOCD_SERVER_LOGFORMAT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.log.format
                optional: true
          - name: ARGOCD_SERVER_LOG_LEVEL
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.log.level
                optional: true
          - name: ARGOCD_SERVER_REPO_SERVER
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: repo.server
                optional: true
          - name: ARGOCD_SERVER_DEX_SERVER
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.dex.server
                optional: true
          - name: ARGOCD_SERVER_DISABLE_AUTH
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.disable.auth
                optional: true
          - name: ARGOCD_SERVER_ENABLE_GZIP
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.enable.gzip
                optional: true
          - name: ARGOCD_SERVER_REPO_SERVER_TIMEOUT_SECONDS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.repo.server.timeout.seconds
                optional: true
          - name: ARGOCD_SERVER_X_FRAME_OPTIONS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.x.frame.options
                optional: true
          - name: ARGOCD_SERVER_CONTENT_SECURITY_POLICY
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.content.security.policy
                optional: true
          - name: ARGOCD_SERVER_REPO_SERVER_PLAINTEXT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.repo.server.plaintext
                optional: true
          - name: ARGOCD_SERVER_REPO_SERVER_STRICT_TLS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.repo.server.strict.tls
                optional: true
          - name: ARGOCD_SERVER_DEX_SERVER_PLAINTEXT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.dex.server.plaintext
                optional: true
          - name: ARGOCD_SERVER_DEX_SERVER_STRICT_TLS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.dex.server.strict.tls
                optional: true
          - name: ARGOCD_TLS_MIN_VERSION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.tls.minversion
                optional: true
          - name: ARGOCD_TLS_MAX_VERSION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.tls.maxversion
                optional: true
          - name: ARGOCD_TLS_CIPHERS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.tls.ciphers
                optional: true
          - name: ARGOCD_SERVER_CONNECTION_STATUS_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.connection.status.cache.expiration
                optional: true
          - name: ARGOCD_SERVER_OIDC_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.oidc.cache.expiration
                optional: true
          - name: ARGOCD_SERVER_LOGIN_ATTEMPTS_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.login.attempts.expiration
                optional: true
          - name: ARGOCD_SERVER_STATIC_ASSETS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.staticassets
                optional: true
          - name: ARGOCD_APP_STATE_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.app.state.cache.expiration
                optional: true
          - name: REDIS_SERVER
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: redis.server
                optional: true
          - name: REDIS_COMPRESSION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: redis.compression
                optional: true
          - name: REDISDB
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: redis.db
                optional: true
          - name: REDIS_USERNAME
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: redis-username
                optional: true
          - name: REDIS_PASSWORD
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: auth
                optional: true
          - name: REDIS_SENTINEL_USERNAME
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: redis-sentinel-username
                optional: true
          - name: REDIS_SENTINEL_PASSWORD
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: redis-sentinel-password
                optional: true
          - name: ARGOCD_DEFAULT_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.default.cache.expiration
                optional: true
          - name: ARGOCD_MAX_COOKIE_NUMBER
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.http.cookie.maxnumber
                optional: true
          - name: ARGOCD_SERVER_LISTEN_ADDRESS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.listen.address
                optional: true
          - name: ARGOCD_SERVER_METRICS_LISTEN_ADDRESS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.metrics.listen.address
                optional: true
          - name: ARGOCD_SERVER_OTLP_ADDRESS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: otlp.address
                optional: true
          - name: ARGOCD_SERVER_OTLP_INSECURE
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: otlp.insecure
                optional: true
          - name: ARGOCD_SERVER_OTLP_HEADERS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: otlp.headers
                optional: true
          - name: ARGOCD_APPLICATION_NAMESPACES
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: application.namespaces
                optional: true
          - name: ARGOCD_SERVER_ENABLE_PROXY_EXTENSION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.enable.proxy.extension
                optional: true
          - name: ARGOCD_K8SCLIENT_RETRY_MAX
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.k8sclient.retry.max
                optional: true
          - name: ARGOCD_K8SCLIENT_RETRY_BASE_BACKOFF
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.k8sclient.retry.base.backoff
                optional: true
          - name: ARGOCD_API_CONTENT_TYPES
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.api.content.types
                optional: true
          - name: ARGOCD_SERVER_WEBHOOK_PARALLELISM_LIMIT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: server.webhook.parallelism.limit
                optional: true
          - name: ARGOCD_APPLICATIONSET_CONTROLLER_ENABLE_NEW_GIT_FILE_GLOBBING
            valueFrom:
              configMapKeyRef:
                key: applicationsetcontroller.enable.new.git.file.globbing
                name: argocd-cmd-params-cm
                optional: true
          - name: ARGOCD_APPLICATIONSET_CONTROLLER_SCM_ROOT_CA_PATH
            valueFrom:
              configMapKeyRef:
                key: applicationsetcontroller.scm.root.ca.path
                name: argocd-cmd-params-cm
                optional: true
          - name: ARGOCD_APPLICATIONSET_CONTROLLER_ALLOWED_SCM_PROVIDERS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: applicationsetcontroller.allowed.scm.providers
                optional: true
          - name: ARGOCD_APPLICATIONSET_CONTROLLER_ENABLE_SCM_PROVIDERS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: applicationsetcontroller.enable.scm.providers
                optional: true
        volumeMounts:
        - mountPath: /app/config/ssh
          name: ssh-known-hosts
        - mountPath: /app/config/tls
          name: tls-certs
        - mountPath: /app/config/server/tls
          name: argocd-repo-server-tls
        - mountPath: /app/config/dex/tls
          name: argocd-dex-server-tls
        - mountPath: /home/argocd
          name: plugins-home
        - mountPath: /shared/app/custom
          name: styles
        - mountPath: /tmp
          name: tmp
        - name: argocd-cmd-params-cm
          mountPath: /home/argocd/params
        ports:
        - name: server
          containerPort: 8080
          protocol: TCP
        - name: metrics
          containerPort: 8083
          protocol: TCP
        livenessProbe:
          httpGet:
            path: /healthz?full=true
            port: server
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 1
          successThreshold: 1
          failureThreshold: 3
        readinessProbe:
          httpGet:
            path: /healthz
            port: server
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 1
          successThreshold: 1
          failureThreshold: 3
        resources:
          {}
        securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          seccompProfile:
            type: RuntimeDefault
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            podAffinityTerm:
              labelSelector:
                matchLabels:
                  app.kubernetes.io/name: argocd-server
              topologyKey: kubernetes.io/hostname
      volumes:
      - name: plugins-home
        emptyDir: {}
      - name: tmp
        emptyDir: {}
      - name: ssh-known-hosts
        configMap:
          name: argocd-ssh-known-hosts-cm
      - name: tls-certs
        configMap:
          name: argocd-tls-certs-cm
      - name: styles
        configMap:
          name: argocd-styles-cm
          optional: true
      - name: argocd-repo-server-tls
        secret:
          secretName: argocd-repo-server-tls
          optional: true
          items:
          - key: tls.crt
            path: tls.crt
          - key: tls.key
            path: tls.key
          - key: ca.crt
            path: ca.crt
      - name: argocd-dex-server-tls
        secret:
          secretName: argocd-dex-server-tls
          optional: true
          items:
          - key: tls.crt
            path: tls.crt
          - key: ca.crt
            path: ca.crt
      - name: argocd-cmd-params-cm
        configMap:
          optional: true
          name: argocd-cmd-params-cm
          items:
          - key: server.profile.enabled
            path: profiler.enabled
      dnsPolicy: ClusterFirst
---
# Source: argo-cd/templates/dex/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: argocd-dex-server
  namespace: argocd
  labels:
    helm.sh/chart: argo-cd-7.7.16
    app.kubernetes.io/name: argocd-dex-server
    app.kubernetes.io/instance: argocd
    app.kubernetes.io/component: dex-server
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/part-of: argocd
    app.kubernetes.io/version: "v2.13.3"
spec:
  replicas: 1
  revisionHistoryLimit: 3
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-dex-server
      app.kubernetes.io/instance: argocd
  template:
    metadata:
      annotations:
        checksum/cmd-params: 319d56ae73721d7d7117931854629353486fc30e0448801c8d6337e46fe9aea0
      labels:
        helm.sh/chart: argo-cd-7.7.16
        app.kubernetes.io/name: argocd-dex-server
        app.kubernetes.io/instance: argocd
        app.kubernetes.io/component: dex-server
        app.kubernetes.io/managed-by: Helm
        app.kubernetes.io/part-of: argocd
        app.kubernetes.io/version: "v2.13.3"
    spec:
      terminationGracePeriodSeconds: 30
      serviceAccountName: argocd-dex-server
      automountServiceAccountToken: true
      containers:
      - name: dex-server
        image: ghcr.io/dexidp/dex:v2.41.1
        imagePullPolicy: IfNotPresent
        command:
        - /shared/argocd-dex
        - --logformat=text
        - --loglevel=info
        args:
        - rundex
        env:
          - name: ARGOCD_DEX_SERVER_LOGFORMAT
            valueFrom:
              configMapKeyRef:
                key: dexserver.log.format
                name: argocd-cmd-params-cm
                optional: true
          - name: ARGOCD_DEX_SERVER_LOGLEVEL
            valueFrom:
              configMapKeyRef:
                key: dexserver.log.level
                name: argocd-cmd-params-cm
                optional: true
          - name: ARGOCD_DEX_SERVER_DISABLE_TLS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: dexserver.disable.tls
                optional: true
        ports:
        - name: http
          containerPort: 5556
          protocol: TCP
        - name: grpc
          containerPort: 5557
          protocol: TCP
        - name: metrics
          containerPort: 5558
          protocol: TCP
        resources:
          {}
        securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          seccompProfile:
            type: RuntimeDefault
        volumeMounts:
        - name: static-files
          mountPath: /shared
        - name: dexconfig
          mountPath: /tmp
        - name: argocd-dex-server-tls
          mountPath: /tls
      initContainers:
      - name: copyutil
        image: quay.io/argoproj/argocd:v2.13.3
        imagePullPolicy: IfNotPresent
        command:
        - /bin/cp
        - -n
        - /usr/local/bin/argocd
        - /shared/argocd-dex
        volumeMounts:
        - mountPath: /shared
          name: static-files
        - mountPath: /tmp
          name: dexconfig
        resources:
          {}
        securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          seccompProfile:
            type: RuntimeDefault
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            podAffinityTerm:
              labelSelector:
                matchLabels:
                  app.kubernetes.io/name: argocd-dex-server
              topologyKey: kubernetes.io/hostname
      volumes:
      - name: static-files
        emptyDir: {}
      - name: dexconfig
        emptyDir: {}
      - name: argocd-dex-server-tls
        secret:
          secretName: argocd-dex-server-tls
          optional: true
          items:
          - key: tls.crt
            path: tls.crt
          - key: tls.key
            path: tls.key
          - key: ca.crt
            path: ca.crt
      dnsPolicy: ClusterFirst
---
# Source: argo-cd/templates/redis/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: argocd-redis
  namespace: argocd
  labels:
    helm.sh/chart: argo-cd-7.7.16
    app.kubernetes.io/name: argocd-redis
    app.kubernetes.io/instance: argocd
    app.kubernetes.io/component: redis
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/part-of: argocd
    app.kubernetes.io/version: "v2.13.3"
spec:
  replicas: 1
  revisionHistoryLimit: 3
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-redis
  template:
    metadata:
      labels:
        helm.sh/chart: argo-cd-7.7.16
        app.kubernetes.io/name: argocd-redis
        app.kubernetes.io/instance: argocd
        app.kubernetes.io/component: redis
        app.kubernetes.io/managed-by: Helm
        app.kubernetes.io/part-of: argocd
        app.kubernetes.io/version: "v2.13.3"
    spec:
      securityContext:
        runAsNonRoot: true
        runAsUser: 999
        seccompProfile:
          type: RuntimeDefault
      terminationGracePeriodSeconds: 30
      serviceAccountName: default
      automountServiceAccountToken: true
      containers:
      - name: redis
        image: public.ecr.aws/docker/library/redis:7.4.1-alpine
        imagePullPolicy: IfNotPresent
        args:
        - --save
        - ""
        - --appendonly
        - "no"
        - --requirepass $(REDIS_PASSWORD)
        env:
        - name: REDIS_PASSWORD
          valueFrom:
            secretKeyRef:
              name: argocd-redis
              key: auth
        ports:
        - name: redis
          containerPort: 6379
          protocol: TCP
        resources:
          {}
        securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          readOnlyRootFilesystem: true
        volumeMounts:
          - mountPath: /health
            name: health
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            podAffinityTerm:
              labelSelector:
                matchLabels:
                  app.kubernetes.io/name: argocd-redis
              topologyKey: kubernetes.io/hostname
      volumes:
        - name: health
          configMap:
            name: argocd-redis-health-configmap
            defaultMode: 493
      dnsPolicy: ClusterFirst
---
# Source: argo-cd/templates/argocd-application-controller/statefulset.yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: argocd-application-controller
  namespace: argocd
  labels:
    helm.sh/chart: argo-cd-7.7.16
    app.kubernetes.io/name: argocd-application-controller
    app.kubernetes.io/instance: argocd
    app.kubernetes.io/component: application-controller
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/part-of: argocd
    app.kubernetes.io/version: "v2.13.3"
spec:
  replicas: 1
  revisionHistoryLimit: 5
  serviceName: argocd-application-controller
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-application-controller
      app.kubernetes.io/instance: argocd
  template:
    metadata:
      annotations:
        checksum/cmd-params: 319d56ae73721d7d7117931854629353486fc30e0448801c8d6337e46fe9aea0
        checksum/cm: 0c6acb003d37749ffaab2d73569f228c33c754ffd773e4cb885f35351713e5b9
      labels:
        helm.sh/chart: argo-cd-7.7.16
        app.kubernetes.io/name: argocd-application-controller
        app.kubernetes.io/instance: argocd
        app.kubernetes.io/component: application-controller
        app.kubernetes.io/managed-by: Helm
        app.kubernetes.io/part-of: argocd
        app.kubernetes.io/version: "v2.13.3"
    spec:
      terminationGracePeriodSeconds: 30
      serviceAccountName: argocd-application-controller
      automountServiceAccountToken: true
      containers:
      - args:
        - /usr/local/bin/argocd-application-controller
        - --metrics-port=8082
        image: quay.io/argoproj/argocd:v2.13.3
        imagePullPolicy: IfNotPresent
        name: application-controller
        env:
          - name: ARGOCD_CONTROLLER_REPLICAS
            value: "1"
          - name: ARGOCD_APPLICATION_CONTROLLER_NAME
            value: argocd-application-controller
          - name: ARGOCD_RECONCILIATION_TIMEOUT
            valueFrom:
              configMapKeyRef:
                name: argocd-cm
                key: timeout.reconciliation
                optional: true
          - name: ARGOCD_HARD_RECONCILIATION_TIMEOUT
            valueFrom:
              configMapKeyRef:
                name: argocd-cm
                key: timeout.hard.reconciliation
                optional: true
          - name: ARGOCD_RECONCILIATION_JITTER
            valueFrom:
              configMapKeyRef:
                key: timeout.reconciliation.jitter
                name: argocd-cm
                optional: true
          - name: ARGOCD_REPO_ERROR_GRACE_PERIOD_SECONDS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.repo.error.grace.period.seconds
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_REPO_SERVER
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: repo.server
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_REPO_SERVER_TIMEOUT_SECONDS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.repo.server.timeout.seconds
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_STATUS_PROCESSORS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.status.processors
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_OPERATION_PROCESSORS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.operation.processors
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_LOGFORMAT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.log.format
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_LOGLEVEL
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.log.level
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_METRICS_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.metrics.cache.expiration
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_SELF_HEAL_TIMEOUT_SECONDS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.self.heal.timeout.seconds
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_SELF_HEAL_BACKOFF_TIMEOUT_SECONDS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.self.heal.backoff.timeout.seconds
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_SELF_HEAL_BACKOFF_FACTOR
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.self.heal.backoff.factor
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_SELF_HEAL_BACKOFF_CAP_SECONDS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.self.heal.backoff.cap.seconds
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_REPO_SERVER_PLAINTEXT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.repo.server.plaintext
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_REPO_SERVER_STRICT_TLS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.repo.server.strict.tls
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_PERSIST_RESOURCE_HEALTH
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.resource.health.persist
                optional: true
          - name: ARGOCD_APP_STATE_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.app.state.cache.expiration
                optional: true
          - name: REDIS_SERVER
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: redis.server
                optional: true
          - name: REDIS_COMPRESSION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: redis.compression
                optional: true
          - name: REDISDB
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: redis.db
                optional: true
          - name: REDIS_USERNAME
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: redis-username
                optional: true
          - name: REDIS_PASSWORD
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: auth
                optional: true
          - name: REDIS_SENTINEL_USERNAME
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: redis-sentinel-username
                optional: true
          - name: REDIS_SENTINEL_PASSWORD
            valueFrom:
              secretKeyRef:
                name: argocd-redis
                key: redis-sentinel-password
                optional: true
          - name: ARGOCD_DEFAULT_CACHE_EXPIRATION
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.default.cache.expiration
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_OTLP_ADDRESS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: otlp.address
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_OTLP_INSECURE
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: otlp.insecure
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_OTLP_HEADERS
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: otlp.headers
                optional: true
          - name: ARGOCD_APPLICATION_NAMESPACES
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: application.namespaces
                optional: true
          - name: ARGOCD_CONTROLLER_SHARDING_ALGORITHM
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.sharding.algorithm
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_KUBECTL_PARALLELISM_LIMIT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.kubectl.parallelism.limit
                optional: true
          - name: ARGOCD_K8SCLIENT_RETRY_MAX
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.k8sclient.retry.max
                optional: true
          - name: ARGOCD_K8SCLIENT_RETRY_BASE_BACKOFF
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.k8sclient.retry.base.backoff
                optional: true
          - name: ARGOCD_APPLICATION_CONTROLLER_SERVER_SIDE_DIFF
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.diff.server.side
                optional: true
          - name: ARGOCD_IGNORE_NORMALIZER_JQ_TIMEOUT
            valueFrom:
              configMapKeyRef:
                name: argocd-cmd-params-cm
                key: controller.ignore.normalizer.jq.timeout
                optional: true
        ports:
        - name: metrics
          containerPort: 8082
          protocol: TCP
        readinessProbe:
          httpGet:
            path: /healthz
            port: metrics
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 1
          successThreshold: 1
          failureThreshold: 3
        resources:
          {}
        securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          seccompProfile:
            type: RuntimeDefault
        workingDir: /home/argocd
        volumeMounts:
        - mountPath: /app/config/controller/tls
          name: argocd-repo-server-tls
        - mountPath: /home/argocd
          name: argocd-home
        - name: argocd-cmd-params-cm
          mountPath: /home/argocd/params
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            podAffinityTerm:
              labelSelector:
                matchLabels:
                  app.kubernetes.io/name: argocd-application-controller
              topologyKey: kubernetes.io/hostname
      volumes:
      - name: argocd-home
        emptyDir: {}
      - name: argocd-repo-server-tls
        secret:
          secretName: argocd-repo-server-tls
          optional: true
          items:
          - key: tls.crt
            path: tls.crt
          - key: tls.key
            path: tls.key
          - key: ca.crt
            path: ca.crt
      - name: argocd-cmd-params-cm
        configMap:
          optional: true
          name: argocd-cmd-params-cm
          items:
          - key: controller.profile.enabled
            path: profiler.enabled
      dnsPolicy: ClusterFirst

NOTES:
In order to access the server UI you have the following options:

1. kubectl port-forward service/argocd-server -n argocd 8080:443

    and then open the browser on http://localhost:8080 and accept the certificate

2. enable ingress in the values file `server.ingress.enabled` and either
      - Add the annotation for ssl passthrough: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-1-ssl-passthrough
      - Set the `configs.params."server.insecure"` in the values file and terminate SSL at your ingress: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-2-multiple-ingress-objects-and-hosts


After reaching the UI the first time you can login with username: admin and the random password generated during the installation. You can find the password by running:

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

(You should delete the initial secret afterwards as suggested by the Getting Started Guide: https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)
@rifaterdemsahin ➜ /workspaces/openshift-argocd/6_Symbols/2_ArgoCd (main) $ 