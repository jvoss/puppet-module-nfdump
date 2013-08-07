# puppet-module-nfdump

A puppet module that installs/configures/manages nfdump.

## Parameters

```ruby
$use_ramdisk::  Boolean. Mounts a ramdisk, uses the $data_base_dir for the base
                 of the RAM disk.
$ramdisk_size:: The size of the RAM disk if $use_ramdisk is true

nfdump options:
$align::           '-w': Boolean. Align file rotation with next minute specified
                         by interval
$bufferlen::       '-B': Integer. Specify the socket input buffer length in bytes.
$compress::        '-z': Boolean. Compress flows. Use fast LZ01X-1 compression
                         in output file
$data_base_dir::   '-l': String. Database dir. Nfdump ignored if using hosts array
$extensions::      '-T': String. List of extensions to be stored in netflow file
$interval::        '-t': Integer. Specifies the time interval in seconds to rotate files
$port::            '-p': Integer. Port number to listen on
$sub_hierarchy::   '-S': Specifies additional directory structure. See 'man nfcapd'
$packet_repeater:: '-R': Array of Strings. Sends all incoming packets to another host.
$hosts::           '-n': Array of Strings. <Ident,IP,base_directory>
```

## Sample Usage:

```ruby
 # Multiple hosts with separate directories and ramdisk
 class { 'nfdump':
   use_ramdisk   => true,
   ramdisk_size  => '512M',

   align         => true,
   bufflen       => 128000,
   compress      => true,
   data_base_dir => '/ramdisk'
   extensions    => 'all',
   interval      => 300,
   port          => 9995,
   sub_hierarchy = 2

   hosts => [ 'host1,192.168.1.1,/ramdisk/host1',
              'host2,192.168.1.2,/ramdisk/host2'
            ]
  }
```

