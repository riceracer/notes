# SciPy

## Read netcdf file

* https://docs.scipy.org/doc/scipy-0.16.1/reference/generated/scipy.io.netcdf.netcdf_file.html

```
from scipy.io import netcdf


class NetCDFWrapper:
    def __init__(self, netcdf_file):
        self.nc_file = netcdf.netcdf_file(netcdf_file, 'r')
        self.data = self.nc_file.variables['myvariable']

    def __enter__(self):
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.data = None
        self.nc_file.close()

    def lookup_myvariable(self, longitude, latitude):
        # scale depends on resolution of the data source
        scale = 25.0
        if longitude == 180.0:
            longitude = -180.0
        latitude = int((latitude + 90.0) * scale)
        longitude = int((longitude + 180.0) * scale)
        return self.data[latitude, longitude]
```
