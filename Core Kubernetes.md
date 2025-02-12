







## 2024-12-27

### C9

 kubelet配置：/etc/containerd/config.toml



## 2024-12-18

1. cgroup
   1. 静态pod: */etc/kubernetes/manifests*



## 2024-12-15

### C4

question:

1. what's the *emptyDir*?

2. *Why can’t the OS use swap in Kubernetes?*

   *predictable manner is more important

   Kubernetes不建议使用swap的主要原因包括以下几点：

   1. performance

   2. ‌container unstable
   3. ‌k8s manage memory
   4. much swap -> node unready‌

   综上所述，Kubernetes不建议使用swap是为了避免性能下降、稳定性问题以及确保资源管理的准确性和节点的稳定性。

3. 内存软限制和硬限制

   在Linux系统中，内存软限制和硬限制是对进程内存使用量的两种限制方式。

   1. ‌内存软限制（Soft Limit）‌：

   是进程当前生效的内存资源限制值。
   进程在运行时，其内存使用量通常不能超过这个软限制。
   进程可以通过系统调用自行修改其软限制，但修改后的值不能超过硬限制。
   当进程尝试使用超过软限制的内存时，系统可能会发出警告，或者根据具体实现，可能会阻止进程继续使用额外的内存。‌

   ‌2. 内存硬限制（Hard Limit）‌：

   是进程所能设定的软限制的最大值，代表了内存使用的最高允许限制。
   硬限制只能由超级用户（root）提升，普通用户无法将硬限制设置得更高。
   硬限制反映了系统对内存资源分配的总体约束，或者管理员为用户或用户组设定的内存使用上限。‌

   这两种限制共同构成了对进程内存使用的双重管控机制。软限制为进程提供了一定的灵活性，允许进程在不超过硬限制的前提下动态调整其内存使用。而硬限制则确保了系统内存资源不会被任意滥用，有助于维持系统的稳定和安全运行。

   在Linux中，可以使用getrlimit和setrlimit系统调用来查询和设置进程的内存软限制和硬限制。‌
   此外，还可以使用ulimit命令在shell会话中限制用户的内存使用，这种限制通常只对当前会话有效，若要使限制持久化，则需要编辑相应的配置文件。‌

4. 如何修改init container的hugepages

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: example-pod
   spec:
     initContainers:
     - name: init-hugepages
       image: busybox
       securityContext:
         privileged: true
       command: ["sh", "-c", "echo 1024 > /proc/sys/vm/nr_hugepages"]
     containers:
     - name: main-container
       image: nginx
       ports:
       - containerPort: 80
   ```

5. kubectl 查看节点资源

   ```
   kubectl get nodes
   kubectl describe nodes <node_name>
   kubectl top nodes
   ```

6. QoS

   ‌Kubernetes中的QoS（Quality of Service）是服务质量的一种控制机制‌，它根据Pod中容器的资源请求（requests）和资源限制（limits）对Pod进行质量划分，并决定在资源不足时哪些Pod应该被优先驱逐或限制资源‌。

   QoS主要分为三个类别：

   ‌Guaranteed‌：

   这类Pod具有最严格的资源限制，并且最不可能面临驱逐‌。
   Pod中的每个容器都必须指定内存和CPU的请求和限制，并且请求必须等于限制‌。
   在资源紧缺时，Guaranteed类别的Pod会最后被考虑驱逐‌。

   ‌Burstable‌：

   这类Pod的资源请求小于资源限制，意味着它们可以在一定程度上超量使用资源‌。
   在资源不足时，相对于Guaranteed类别的Pod，Burstable类别的Pod更有可能被驱逐或限制资源‌。

   ‌BestEffort‌：

   这类Pod没有指定资源请求或限制，或者只指定了部分资源的请求‌。
   在资源紧缺时，BestEffort类别的Pod会首先被考虑驱逐，因为它们没有明确的资源保证‌。

   Kubernetes使用QoS机制来确保在资源有限的情况下，能够优先保障高服务质量Pod的运行，同时合理管理低服务质量Pod的资源使用，以维护集群的整体稳定性和性能‌。

   这种机制特别有助于在节点资源不足或过载时，通过QoS类别来做出决策，确保关键应用的稳定运行‌。

   

7. what is kind? k8s
8. ‌当使用systemd作为容器的初始化系统时，systemd会成为容器的父进程，而不是Docker守护进程‌。

在Docker容器中，通常Docker守护进程（daemon）会作为容器的父进程来启动和管理容器。然而，在某些情况下，比如使用systemd作为容器的初始化系统时，systemd会接管这一角色，成为容器的父进程。这意味着，容器内的进程将直接由systemd管理，而不是由Docker守护进程直接管理。

这种情况通常发生在需要更复杂的进程管理或初始化逻辑时，例如，在容器中运行需要特定初始化顺序或多个服务的应用程序时。通过使用systemd，可以更容易地管理这些服务的启动顺序和依赖关系，从而提高容器的稳定性和可靠性。

需要注意的是，当systemd成为容器的父进程时，Docker守护进程仍然负责容器的整体管理和生命周期控制，包括容器的创建、启动、停止和删除等。systemd则主要负责容器内部进程的管理和初始化。这种分工使得Docker和systemd能够各自发挥其优势，共同为容器提供强大而灵活的管理功能‌。


1. prometheus, cadviser
2. OCI
3. *kube-reserved - system-reserved*区别?
   1. kubelet, kube-proxy
   2. system process
   3. systemd -> containerd, kubelet, kube-proxy