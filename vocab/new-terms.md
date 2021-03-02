# New terms used in context extensions and prototypes that have no RDF or other vocabulary


## ControlPoints
A ControlPoint is a set of pairs <PixelCoords, GeoJSON Point>.

## PixelCoords
PixelCoords contain a single pixel coordinate point that represents a control point for converting between geospatial coordinates and pixel coordinates in Web Map systems.  The geocoordinates are found inside the "value" property.  

## pixel_coords
A single pixel coordinate point that represents a control point for converting between geospatial coordinates and pixel coordinates in Web Map systems.

## georeferencing
A motivation or purpose.  This can be on the Annotation as a motivation or within the body of an Annotation as a purpose.  This lets clients know that this Annotation will contain the data required to georeference the targeted resource into WGS84 space.  
