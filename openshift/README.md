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

Lista todos los nodos con `kubectl get nodes`

## Pod
Un Pod en Kubernetes es un objeto que define una **carga de trabajo**. Es decir, un Pod es uno o varios contenedores que son ejecutados conjuntamente en Kubernetes.

Crea un pod con `kubectl apply -f pod-tomcat.yaml`

Lista todos los pod con `kubectl get pod`

Ver la descripción del pod:  `kubectl describe pod tomcat`

## Deployments
El objeto Deployment define una aplicación con varias réplicas. El Deployment a su vez crea y gestiona los pods que corresponden a esa definición.

Crea un deployment con `kubectl apply -f deployment-tomcat.yaml`

Lista todos los deployment con `kubectl get deploy`
