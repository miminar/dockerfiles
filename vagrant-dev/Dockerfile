FROM fedora:26

ARG vagrant_libvirt_version=latest

RUN dnf install -y @'Development Tools' ruby-devel vagrant redhat-rpm-config libvirt-devel gcc-c++ ansible zlib-devel && dnf clean all
RUN vagrant plugin install vagrant-hostmanager vagrant-mutate vagrant-timezone
RUN if [[ "${vagrant_libvirt_version}" != "latest" ]]; then verarg="--plugin-version ${vagrant_libvirt_version}"; fi; \
    vagrant plugin install ${verarg} vagrant-libvirt
RUN ref="master"; \
    if [[ "${vagrant_libvirt_version}" != "latest" ]]; then ref="${vagrant_libvirt_version}"; fi; \
    ver="$(vagrant plugin list | sed -n 's/^vagrant-libvirt\s*(\([^)]\+\)).*/\1/p' | head -n 1)"; \
    curl "https://github.com/vagrant-libvirt/vagrant-libvirt/compare/${ref}...miminar:smarter-find-host-ip-for-nfs-mount-${ver}.patch" | \
      patch -d "${HOME}/.vagrant.d/gems/gems/vagrant-libvirt-${ver}" -p1
RUN mkdir /vagrant
WORKDIR /vagrant 
CMD ["/usr/bin/vagrant"]
