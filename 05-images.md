### Images

The image is generalised (sysprep) before uploading to glance.


- virt-sysprep :
    - removes any unique settings on the image
 

#### Uploads

1. Using Horizon or
2. Using the CLI
    - openstack image create --format qcow2 --file (path/to/file)

- cloud-init:
    - To customise / bootstrap an image

#### Minimum Requirements



#### Glance image location

/vat/lib/glance/images