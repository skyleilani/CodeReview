# CodeReview
Code review of a very basic mandelbrot shader explorer built in unity and embedded in a webpage

[Explore Mandelbrot Fractal Shader Here](f05unt.csb.app/)

#### mandelbrot code snippet from mandelbrot.glslf ####
```
fixed4 frag(v2f i) : SV_Target
            {
                // mandelbrot fractal algorithm  
                // Z = Z^2 + C
                
                // start position of pixel, initialized to coordinate of pixel we're focused on   
                float2 C = _Area.xy + (i.uv - 0.5) * _Area.zw; 
                
                C = rotate(C, _Area.xy, _Angle);
                
                // current pos of pixel (updates)
                float2 z;

                for (float i = 0; i < 255; i++) {

                    // update pixel position based on previous pixel position 
                    // ((z.x^2 * z.y^2),    (2(z.x) * z.y)) + Start position
                    //  (updated_x     ,  updated_y ) + C
                    // Z^2 + C 
                    
                    z = float2(z.x * z.x - z.y * z.y, 2 * z.x * z.y) + C; // Z = Z_SQ

                    // breakout of loop
                    if (length(z) > 2) break;
                }

                float4 result = sin(float4(0.15f, 0.08f, 25, 1) * i/20);
                return result;
            }
 ```
 ### context & explanation ### 
 
 for reference, the equation for the mandelbrot fractal is 
 *Z = Z^2 + C*
 
 The code snippet above is the core of this mandelbrot explorer, as without it we have no mandelbrot to explore. 
 It's a fragment shader, so it's essentially placing potential pixels based on this iterative function we have. 
 
 This is an Image Effect shader written in Open GL Shading Language (GLSL) rendered in Unity. 
 
 The movement (ability to use WASD keys to navigate the fractal) is written in a C# script. 
 
 Both the fragment shader and the C# script are attached to the same Canvas( which largely focuses on 2D graphics and UI elements positioned in Unity's 3D space )
 
 
