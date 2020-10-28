# OpenShift

OpenShift es una distribución de Kubernetes que añade funcionalidades centradas en la automatización, seguridad y *developer experience*.

Es una distribución propietaria de RedHat, muy utilizada a nivel empresarial por estas nuevas capas y por el soporte de esta compañía.

Puede ser desplegada en cualquier entorno (cloud, on-premise, local).

También puedes verla como OCP (OpenShift Container Platform)

Sitio web oficial: [https://www.openshift.com](https://www.openshift.com)

### Kubernetes

Kubernetes es un **orquestador de contenedores**:

- Administra el despliegue de contenedores
- Preparado para entornos de producción

Kubernetes dispone de herramientas para levantar contenedores:

- En alta disponibilidad
- De forma segura
- Aislados de otras cargas de trabajo
- Conectados entre sí
- Expuestos a Internet
- Conectados con servicios en la nube

- [¿Qué es Kubernetes? Web oficial](https://kubernetes.io/es/docs/concepts/overview/what-is-kubernetes/)
- [Cómic](https://cloud.google.com/kubernetes-engine/kubernetes-comic)
- [Guía ilustrada](https://www.cncf.io/wp-content/uploads/2020/08/The-Illustrated-Childrens-Guide-to-Kubernetes.pdf)


### OKD

OKD es la distribución de Kubernetes en la que se basa OpenShift. La principal diferencia entre ambos es que OKD es la distribución de código abierto, y sobre ella RedHat añade la capa de funciones *enterprise* que forman Openshift.

La arquitectura de ambas es exactamente la misma y todas las aplicaciones son compatibles. Puedes desplegar OKD de forma gratuita en cualquier entorno compatible. Las versiones de Openshift y OKD van de la mano.s

Anteriormente era llamada OpenShift Origin, es posible que aún veáis ese término.

Sitio web oficial: [https://www.okd.io](https://www.okd.io)

Diferencas entre Kubernetes, OKD y OpenShift: [https://www.openshift.com/learn/topics/kubernetes](https://www.openshift.com/learn/topics/kubernetes)

Más diferencias entre Kubernetes y OKD/OpenShift: [https://cloudowski.com/articles/10-differences-between-openshift-and-kubernetes](https://cloudowski.com/articles/10-differences-between-openshift-and-kubernetes)

### Versiones

Actualmente hay dos versiones con soporte: v3 y v4. Las aplicaciones desplegadas en cualquiera de ellas son completamente compatibles entre sí. Las mayores diferencias son a nivel de arquitectura y despliegue, nuevas funcionalidades en todos los campos, y una experiencia de usuario reformada.

Novedades de la v4:
- [https://www.openshift.com/blog/introducing-red-hat-openshift-4](https://www.openshift.com/blog/introducing-red-hat-openshift-4)
- [https://docs.okd.io/latest/whats_new/new-features.html]()

### Distribuciones para local

Minishift: Es OKD v3 para levantar en local. Crea una máquina virtual con una distribución de OKD v3 atuomáticamente.

CodeReady Containers (CRC): Es la v4. El funcionamiento es exactamente igual (una máquina virtual en local que levanta la plataforma), pero en este caso permite levantar tanto OpenShift con todas las funciones, como OKD.

CRC OpenShift: [https://developers.redhat.com/products/codeready-containers/overview](https://developers.redhat.com/products/codeready-containers/overview)

CRC OKD: [https://www.okd.io/crc.html](https://www.okd.io/crc.html)


### oc CLI

OpenShift incluye su propio CLI aparte de `kubectl`. Los comandos de ambos son prácticamente iguales, `oc` añade algunas funcionalidades interesantes e incluye todo lo necesario para trabajar con los objetos propios de OpenShift.

Instalación de oc: [https://docs.openshift.com/container-platform/4.5/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli](https://docs.openshift.com/container-platform/4.5/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli)

### Componentes más importantes incluidos con OpenShift

[Docker Registry privado](https://docs.openshift.com/container-platform/4.5/registry/architecture-component-imageregistry.html)

[Operators](https://docs.openshift.com/container-platform/4.5/operators/understanding/olm-what-operators-are.html) (v4)

[Service Mesh](https://docs.openshift.com/container-platform/4.5/service_mesh/v1x/servicemesh-release-notes.html)  (v4)

[Monitorización](https://docs.openshift.com/container-platform/4.5/monitoring/cluster_monitoring/about-cluster-monitoring.html)


# Comandos básicos con oc

Conectarse a un clúster: `oc login -u <USER> -p <PASSWORD> <URL>`

Crear un proyecto: `oc new-project <PROJECT>`

Listar proyectos a los que tengo acceso: `oc projects`

Cambiar de proyecto: `oc project <PROJECT>`

Crea objetos a partir de un archivo YAML: `oc apply -f <FILE>`

Eliminar objetos a partir de un archivo YAML: `oc delete -f <FILE>`

Listar cualquier objeto: `oc get <TYPE>`

Inspeccionar un objeto en concreto: `oc get <TYPE> <NAME>` `oc get <TYPE> <NAME> -o yaml`

Ver la descripción y eventos de un objeto en concreto: `oc describe <TYPE> <NAME>`


# Objetos de Kubernetes y OpenShift (y OKD)

## Nodos

Son los servidores físicos que forman parte del clúster.

Lista todos los nodos con `oc get nodes`

## Pod

Un Pod en Kubernetes es un objeto que define una **carga de trabajo**. Es decir, un Pod es uno o varios contenedores que son ejecutados conjuntamente en Kubernetes.

Crea un pod con `oc apply -f pod-tomcat.yaml`

Lista todos los pod con `oc get pod`

Ver la descripción del pod:  `oc describe pod tomcat`

## Deployments

El objeto Deployment define una aplicación con varias réplicas. El Deployment a su vez crea y gestiona los pods que corresponden a esa definición.

Crea un deployment con `oc apply -f deployment-tomcat.yaml`

Lista todos los deployment con `oc get deploy`

## DeploymentConfig

Similar to deployment. deploymentConfig es un objeto propio de Openshift que da todas las funcionalidades del objeto deployment y añade en el `spec` el campo `triggers`, con el que podemos hacer que el deploymentConfig actualice automáticamente sus pods cuando observa cambios en una imagen de Docker por ejemplo.


Crea un deployment con `oc apply -f deployment-config-petclinic.yaml`

Lista todos los deployment con `oc get dc`

## DaemonSet

El objeto DaemonSet despliega un pod (solo uno) en cada nodo del clúster

Crea un DaemonSet con `oc apply -f daemonset.yaml`

Lista todos los DaemonSet con `oc get ds`

## Statefulset

El objeto Statefulset define una aplicación que tiene datos persistentes en disco (por ejemplo una base de datos). Es prácticamente igual que el deployment, pero levanta los pods siempre con un nombre fijo de forma que los datos pueden persistir entre despliegues y reinicios.

Crea un statefulset con `oc apply -f statefulset.yaml`

Lista todos los statefulset con `oc get statefulset`

## Job

El objeto Job define una carga de trabajo puntual, una tarea que finalizará con éxito en algún momento.

Crea un job con `oc apply -f job.yaml`

Lista todos los job con `oc get job`

## CronJob

El objeto CronJob crea jobs de forma periódica. Por ejemplo, todas las noches, para ejecutar tareas cada cierto tiempo

Crea un job con `oc apply -f cronjob.yaml`

Lista todos los job con `oc get cronjob`

## Service

Service representa un balanceador de carga entre varios pods que comparten una misma etiqueta, normalmente entre las réplicas de un mismo deployment o statefulset

Crea un service con `oc apply -f service-tomcat.yaml`

Lista todos los service con `oc get service`

## Route

Permite configurar el router incluido con OpenShift para que dirija tráfico a tu aplicación. El router expone una IP pública, hacia la que se puede dirigir cualquier dominio. Con un Route se define qué dominio deber ser dirigido a tu servicio en concreto. También se pueden configurar distintas rutas y dividir el tráfico entre distintos servicios.

Puedes crear un Route con `oc apply -f route.yaml`

Referencia de todas las posibilidades de Route: [https://docs.openshift.com/container-platform/4.5/welcome/index.html](https://docs.openshift.com/container-platform/4.5/welcome/index.html)

## ConfigMap

Configmap contiene una o varias variables que más adelante se pueden montar en cualquier carga de trabajo.

Crea un service con `kubectl apply -f configmap.yaml`

Lista todos los service con `kubectl get configmap`

Puedes crear un configMap a partir de un archivo o carpeta con `kubectl create configmap`

En el ejemplo `deployment-petclinic.yaml` tienes un ejemplo de cómo montar un configMap como volumen y como variables de entorno.

## Secret

Similar a configmap, pero los datos se almacenan codificados en base64

Crea un service con `kubectl apply -f secret.yaml`

Lista todos los service con `kubectl get secret`

Puedes crear un secret a partir de un archivo o carpeta con `kubectl create secret generic`

También puedes crear un secret especial con las credenciales para acceder a registries privados:

`kubectl create secret docker-registry`

## PersistentVolume

Un persistentVolume representa un disco persistente de cualquier tipo que está disponible para ser utilizado en Kubernetes.

Lo habitual no es crear estos persistentVolume de forma manual sino que una storageClass los cree automáticamente cuando detecta un nuevo persistentVolumeClaim

Crea un persistentVolume con `kubectl apply -f persistentvolume.yaml`

Lista todos los persistentVolume con `kubectl get pv`


## PersistentVolumeClaim
Un persistentVolumeClaim representa una petición de disco persistente, con ciertos requisitos de tamaño y modos de acceso. Éstos son asociados con pod para habilitar persistencia de datos a sus contenedores. Kubernetes asociará un persistentVolumeClaim con un persistentVolume que cumpla sus requisitos.

Crea un persistentVolumeClaim con `kubectl apply -f persistentvolumeclaim.yaml`

Lista todos los persistentVolumeClaim con `kubectl get pvc`


## ServiceAccount

Representa un token de autenticación que puede ser montado en los pods. Este token sirve para autenticar las peticiones que realice ese pod hacia el propio cluster de OpenShift. Con Roles y RoleBindings se puede dar permisos a esta serviceAccount para que interactúa con otros recursos del clúster.

En todos los proyectos/namespaces existe una serviceAccount `default` que ser monta por defecto en todos los pods a menos que se especifique una distinta.


## BuildConfig

Define todo lo relativo a la construcción de un proyecto. En concreto tiene la información sobre el origen del código (`source`), la estrategia o método para construirlo (`strategy`) y el resultado (`output`), que en todo caso será siempre una imagen de Docker.

Puedes crear una buildConfig con `oc apply -f bc-petclinic.yaml`

Una BuildConfig puede construir:
* Dockerfiles con la estrategia `dockerStrategy`
* Contenedores a partir de imágenes preparadas para source2image con la estrategia `sourceStrategy`
* Ejecutar simplemente un contenedor personalizado con la estrategia `customStrategy`
* Jenkinsfiles, con la estrategia `jenkinsPipelineStrategy`

Referencia de las estrategias posibles: [https://docs.openshift.com/container-platform/4.5/builds/build-strategies.html](https://docs.openshift.com/container-platform/4.5/builds/build-strategies.html)

En los archivos que comienzan con `bc-.....yaml` tienes ejemplos de cada una de ellas.

## Build 

Es simplemente una ejecución de una buildConfig

Puedes lanzar una build con `oc start-build`


## ImageStream

Representa una imagen de Docker presente en el registry interno de OpenShift. Nos permite abstraernos de la conexión con el registry.

En `bc-petclinic.yaml` creamos y utilizamos imageStream en una buildConfig

## HorizontalPodAutoscaling

Con este objeto configuramos el autoescalado de un Deployment o StatefulSet. En él se espcifican los parámetros del autoescalado como el máximo y mínimo número de réplicas y las métricas y targets que dispararan el autoescalado.

Crea un HorizontalPodAutoscaling con `kubectl apply -f hpa-petclinic.yaml`

Lista todos los HorizontalPodAutoscaling con `kubectl get hpa`

# Componentes importantes de OpenShift

## Docker Registry

## Router

# Source2Img (S2I)

# Helm