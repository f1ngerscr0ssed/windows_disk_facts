# windows_disk_facts

#### Table of Contents

1. [Description](#description)
1. [Facts](#facts)
1. [Usage](#usage)



## Description

This module adds  the following facts on Windows:

### `$::disks`

The output of the Powershell `Get-Disk` command, but in a more Puppet-friendly format

### `$::drives`

The output of the Powershell `Get-PSDrive -PSProvider 'FileSystem'` command, but in a more Puppet-friendly format + additional drive type information ('Fixed' = local hard drive, 'Removable' = removable devices like floppy and usb, 'CD-ROM' = optical drives)

### `$::partitions`

The output of the Powershell `Get-Partition` command, but in a more Puppet-friendly format

## Facts

```puppet

disks
{
    0 => 
    {
        partition_style => MBR, 
        provisioning_type => Fixed, 
        operational_status => Online, 
        health_status => Healthy, 
        bus_type => SCSI, 
        unique_id_format => EUI64, 
        offline_reason => , 
        allocated_size => 42949672960, 
        boot_from_disk => true, 
        firmware_version => 0001, 
        friendly_name => Red Hat VirtIO SCSI Disk Device, 
        guid => , is_boot => true, 
        is_clustered => false, 
        is_offline => false, 
        is_read_only => false, 
        is_system => true, 
        largest_free_extent => 0, 
        location => PCIROOT(0)#PCI(0400)#SCSI(P00T00L00), 
        logical_sector_size => 512, 
        manufacturer => Red Hat , 
        model => VirtIO, 
        number => 0, 
        number_of_partitions => 1, 
        object_id => \\?\scsi#disk&ven_red_hat&prod_virtio#4&35110308&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}, 
        path => \\?\scsi#disk&ven_red_hat&prod_virtio#4&35110308&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}, 
        physical_sector_size => 512, 
        serial_number => , 
        signature => 2963357585, 
        size => 42949672960, 
        unique_id => 3141463431303031, 
        ps_computer_name => 
        }
}

drives
{
    C => 
    {
    name => C, 
    root => C:\, 
    description => Windows, 
    maximum_size => , 
    display_root => , 
    used_bytes => 34760683520, 
    free_bytes => 8186888192, 
    drivetype => Fixed
    }
}

partitions
{
    operational_status => Online, 
    type => IFS, 
    access_paths => [C:\, \\?\Volume{91934dc9-99fb-11e7-80d1-806e6f6e6963}\], 
    disk_id => \\?\scsi#disk&ven_red_hat&prod_virtio#4&35110308&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}, 
    disk_number => 0, 
    drive_letter => C, 
    gpt_type => , 
    guid => , 
    is_active => true, 
    is_boot => true, 
    is_hidden => false, 
    is_offline => false, 
    is_read_only => false, 
    is_shadow_copy => false, 
    is_system => true, 
    mbr_type => 7, 
    no_default_drive_letter => false, 
    offset => 1048576, 
    partition_number => 1, 
    size => 42947575808, 
    transition_state => 1, 
    ps_computer_name => 
}

```

## Usage

```puppet
# Loop over all of the partitions and find the one that is mounted to C:\
$::partitions.each |$partition| {
  if $partition['drive_letter'] == 'C' {
    # Do something here
  }
}

# Get the free size of C:\
notice($::drives['C']['free_bytes'])
```

## Contributors

  - [nicolasvan](https:///github.com/nicolasvan)
  - [natemccurdy](https:///github.com/natemccurdy)
  - [covidium](https:///github.com/covidium)
