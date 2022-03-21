# CodeReview
Code review of a very basic mandelbrot shader explorer built in unity and embedded in a webpage


#### mandelbrot code snippet ####
```
fixed4 frag(v2f i) : SV_Target
            {
                 // mandelbrot fractal algorithm  
                // V = V^2 + C
                // start position of pixel, initialized to uv coordinate. 
                float2 C = _Area.xy + (i.uv - 0.5) * _Area.zw; // .zw = last two coords (x, y, z, w) from _Area (4, 4) 
                C = rotate(C, _Area.xy, _Angle);
                // keep track of where pixel is jumping across the string
                float2 z;

                for (float i = 0; i < 255; i++) {

                    // update pixel position based on previous pixel position 
                    // ((z.x^2 * z.y^2),    (2(z.x) * z.y)) + Start position
                    //  (updated_x     ,  updated_y ) + C
                    // Z^2 + C 
                    z = float2(z.x * z.x - z.y * z.y, 2 * z.x * z.y) + C;

                    // breakout of loop
                    if (length(z) > 2) break;
                }

                float4 result = sin(float4(0.15f, 0.08f, 25, 1) * i/20);
                return result;
            }
 ```
 ### context & explanation ### 
 
 for reference, the equation for the mandelbrot fractal is 
 V = V^2 + C
 
 
 
 
