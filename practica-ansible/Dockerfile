FROM ubuntu:22.04

# Se evitan preguntas interactivas durante la instalación de paquetes
ENV DEBIAN_FRONTEND=noninteractive

# openssh-server permite que Ansible se conecte; sudo y python3 son
# necesarios porque Ansible ejecuta sus módulos con Python en el servidor remoto
RUN apt-get update && \
    apt-get install -y openssh-server sudo python3 && \
    mkdir -p /var/run/sshd

# Usuario "ansible" con contraseña "ansible"
RUN useradd -m -s /bin/bash ansible && \
    echo "ansible:ansible" | chpasswd

# Sudo sin contraseña: Ansible no puede escribir contraseñas durante la ejecución
RUN echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible && \
    chmod 0440 /etc/sudoers.d/ansible

EXPOSE 22

# Se deja sshd en primer plano para que el contenedor no se cierre
CMD ["/usr/sbin/sshd", "-D"]