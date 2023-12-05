## December 2024 Allmaps Georeference Annotation Review
By: Bryan Haberberger  
GitHub: https://github.com/thehabes  
Contact: bryan.j.haberberger@slu.edu | thehabes@habesoftware.rocks  

Example Provided : https://new.annotations.allmaps.org/maps?limit=10  

Example Downloaded : [dec-2024-annotations.json](/prototypes/dec-2024-annotations.json)

### @context considerations
```
{
   "type":"AnnotationPage",
   "@context":[
      "http://www.w3.org/ns/anno.jsonld"
   ],
   "items":[
      {
         "id":"https://new.annotations.allmaps.org/maps/131d7a95eeb9e9a5",
         "type":"Annotation",
         "@context":[
            "http://iiif.io/api/extension/georef/1/context.json",
            "http://iiif.io/api/presentation/3/context.json"
         ]
   ...

```
Only the top level object (the AnnotationPage) should have the `@context` property and its value should be
```
"@context":"http://iiif.io/api/extension/georef/1/context.json"
```
The context "http://iiif.io/api/extension/georef/1/context.json" already specifically scopes in "http://www.w3.org/ns/anno.jsonld".  Therefore, you should never have to include "http://www.w3.org/ns/anno.jsonld" anywhere in these Annotations and Annotation Pages because they will have the Georeference Annotation context.  

Only Annotations and Annotation Pages that target a IIIF Presentation API Defined Type (Collection, Manifest, Range, Canvas) or IIIF Image API resource (Image, Fragment, SpecificResoure) should include the IIIF Presentation API context "http://iiif.io/api/presentation/3/context.json". Only in these cases, the context should be
```
"@context":[
   "http://iiif.io/api/extension/georef/1/context.json",
   "http://iiif.io/api/presentation/3/context.json"
]
```
> Note that including extra, duplicated, or unused context is not an error but may cause warnings during JSON-LD processing.

### `id` and `@id` negotation
Noting that you use `id` throughout, but for your SpecificResources you use `@id`.  
```
"type":"SpecificResource",
"source":{
   "@id":"https://tile.loc.gov/image-services/iiif/service:gmd:gmd382:g3824:g3824g:cw0357200",
   "type":"ImageService2",
   "height":9851,
   "width":8597
}
```
Though not techincally an error, you will want to be careful of this in IIIF scenarios.  It can trick a viewer that has not been coded to negotiate between `id` and `@id`.

### `allmaps` property as a foreign member
The `allmaps` property is a foreign member, as it is not described by "http://iiif.io/api/extension/georef/1/context.json".  This is not a problem, but consider noting it as a foreign member via the `_` convention, like `_allmaps`.  It would be wise to include a context for this property, but it is not required.
```
"allmaps":{
   "@context": "https://allmaps.org/wise_context_for_allmaps_property"
   "version":"https://new.annotations.allmaps.org/maps/4f482a5db9ac5581@77cbdfa0621354fa",
   "createdAt":"2022-07-10T08:00:46.732Z",
   "updatedAt":"2022-07-10T08:00:46.732Z",
   "scale":0.001034,
   "area":179605609616361.9,
   "tags":[
      
   ]
}
```

### `transformation` property
None of the Annotations reviewed contained a `transformation` property.  This may have been intentional, just noting it.
```
"transformation": {
 "type": "polynomial",
 "options": {
   "order": 1
 }
}
```
