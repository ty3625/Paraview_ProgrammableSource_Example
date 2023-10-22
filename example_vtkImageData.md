Following code is modified from "5.2.4. Reading binary 2D image" of "https://docs.paraview.org/en/latest/ReferenceManual/pythonProgrammableFilter.html".

The code is for Sources->Programmable source.
Ensure that the `Output Data` Set Type is set to `vtkImageData`.

```python
# Code for 'Script'
import numpy as np

# read raw binary data.
# ensure 'dtype' is set properly.
data = np.zeros([48*62*42], dtype=np.uint8)

dims = [48, 62, 42]
assert data.shape[0] == dims[0]*dims[1]*dims[2], "dimension mismatch"

output.SetExtent(0, dims[0]-1, 0, dims[1]-1, 0, dims[2]-1)
output.PointData.append(data, "scalars")
output.PointData.SetActiveScalars("scalars")
```


```python
# Code for 'RequestInformation Script'.
executive = self.GetExecutive()
outInfo = executive.GetOutputInformation(0)
# we assume the dimensions are (48, 62, 42).
outInfo.Set(executive.WHOLE_EXTENT(), 0, 47, 0, 61, 0, 41)
outInfo.Set(vtk.vtkDataObject.SPACING(), 1, 1, 1)
```
