<!------------------------------------------------------------------- [ Virtualization ] --->
## Virtualization

#### <span class="red">Hardware support</span>
    Intel : lscpu | grep vmx
    AMD   : lscpu | grep svm
    
    lscpu | grep hypervisor

#### <span class="red">Type</span>

    Type 1 : KVM | Xen | Hyper-V
    Type 2 : virtualbox | vmware

#### <span class="red">Config</span>
    cat /etc/machine-id
    cat /var/lib/dbus/machine-id
    dbus-uuidgen --ensure

#### <span class="red">Container</span>
    Doucker



