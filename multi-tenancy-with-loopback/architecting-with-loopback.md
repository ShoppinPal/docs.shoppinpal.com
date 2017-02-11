#Multi Tenant Architecture with Loopback
![](/assets/multi-tenant-architecture.png)


#Relationships
* Users -> `Belongs To` - Organization
* Organization -> `Has Many` - Users


* Products -> `Belongs To` - Organization
* Organization -> `Has Many` - Products


* Catalog -> `Belongs To` - Organization
* Organization -> `Has Many` - Catalog


* Orders -> `Belongs To` - Organization
* Organization -> `Has Many` - Orders









