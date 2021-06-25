Códecs audio/video
------------------

.. note::

  * Requisitos: 
    * Tener instalado los repositorios [[linux:fedora:guides:repos#rpm_fusion|RPM Fusion]]

Instalación
###########

.. code-block:: bash

  sudo dnf install gstreamer-plugins-ugly.x86_64 gstreamer1-plugins-bad-free-extras.x86_64 \
  gstreamer1-plugins-good-extras.x86_64 gstreamer1-vaapi.x86_64 
  sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
  sudo dnf groupupdate sound-and-video
