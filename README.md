# Geometry Shader Cookbook
The repository is the practice project of Geometry shader in Unity engine.

## Define the Method of Geometry Shader
    #pragma geometry geom

## Define Data Structure
    //The data structure from the application to the vertex shader.
    struct a2v  
    {  
        float4 vertex : POSITION;  
        float2 uv : TEXCOORD0;  
    };  
  
    //The data structure from the vertex shader to the geometry shader.
    struct v2g  
    {  
        float4 vertex : POSITION;  
        float2 uv : TEXCOORD0;  
    };
    
    //The data structure from the geometry shader to the fragment shader.
    struct g2f
    {  
        float4 vertex : SV_POSITION;  
        float2 uv : TEXCOORD0;
    };  

## Write Geometry Shader 
      [maxvertexcount(3)]  
      void geom(triangle v2g input[3], inout TriangleStream<g2f> outStream)  
      {  
            g2f o;  
  
            for(int i = 0; i < 3; i++)  
            {  
                  o.vertex = UnityObjectToClipPos(input[i].vertex);  
                  o.uv = input[i].uv;  
                  outStream.Append(o);  
            }  
      
            outStream.RestartStrip();  
      }

| Attribute              |                                                   |
|------------------------|---------------------------------------------------|
| maxvertexcount(number) | The output vertex number for the geometry shader. |

| Inputs      |                                                          |
|-------------|----------------------------------------------------------|
| point       | The point pritimive data.                                          |
| line        | The line pritimive data.                                           |
| lineadj     | The line pritimive data, including the adjacent line pritimive data.         |
| triangle    | The triangle pritimive data.                                       |
| triangleadj | The triangle pritimive data, including the adjacent triangle pritimive data. |

| Outputs                |                           |
|------------------------|---------------------------|
| PointStream<struct>    | The point stream data.    |
| LineStream<struct>     | The line stream data.     |
| TriangleStream<struct> | The triangle stream data. |
    
| Stream Methods |                                                                                                                     |
|----------------|---------------------------------------------------------------------------------------------------------------------|
| Append(struct) | The method to add the data.                                                                                         |
| RestartStrip() | If the output is TriangleStream, you need to call the method to form the triangle. (Three vertices form a triangle) |
  
## Implement Examples
PointStream/Vertex
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_PointStream_Vertex.jpg"></p>
LineStream/Line
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_LineStream_Line.jpg"></p>
TriangleStream/DoNothing
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_DoNothing.jpg"></p>
TriangleStream/ExtrudeVertex
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudeVertex.jpg"></p>
TriangleStream/TriangleAnimation
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_TriangleAnimation.jpg"></p>
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_TriangleAnimation.gif"></p>
TriangleStream/ExtrudePyramid
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudePyramid.jpg"></p>
TriangleStream/ExtrudePyramidAnimation
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudePyramidAnimation.jpg"></p>
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudePyramidAnimation.gif"></p>
TriangleStream/ExtrudeTriangle
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudeTriangle.jpg"></p>
TriangleStream/ExtrudeTriangleAnimation
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudeTriangleAnimation.jpg"></p>
<p align="center"><img style="margin:auto;" src="https://github.com/ted10401/GeometryShaderPractice/blob/master/GithubResources/Custom_Geometry_TriangleStream_ExtrudeTriangleAnimation.gif"></p>
