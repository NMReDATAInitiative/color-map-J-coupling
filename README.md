# color-map-J-coupling
Color map for J coupling (for J-graph and other color-coded representation of NMR H-H scalar coupling constants

It has been carefully thought through in order to provide a large color contrast for values that are particularily significant.

First line: 0 Hz
Second line: 2 Hz
Last (line 11): 20 Hz
## Black background
```
double colormapBlackBackground[] = {
0, 1, 1, 
0, 1, 0, 
1, 1, 0, 
1, 0.5, 0, 
1, 0, 0, 
1, 0, 0.5, 1, 
0, 1, 0.5, 
0, 0.9, 0.2, 
0.2, 1, 0.4, 
0.4, 0.5, 
1, 1, 1,
};
```  
## White background
```
double colormapWhiteBackground[] = {
0, 1, 1, 
0, 1, 0, 
0.8, 0.8, 0, 
0.9, 0.4, 0, 
1, 0, 0, 
1, 0, 0.5, 
1, 0, 1, 
0.5, 0, 1, 
0, 0, 1, 
0, 0, 0.5, 
0, 0, 0,
};
```

<table>
		<tr>
			<th>J </th>
			<th>(R G B) </th>
			<th>(R G B) </th>
		</tr>
		<tr>
			<td> 0 Hz</td>
			<td> <span style="color:#00FFFF;background:black;">(0 1 1)</span> </td>
			<td> <span style="color:#00FFFF;background:white;">(0 1 1)</span> </td>
		</tr>
		<tr>
			<td> 2 Hz</td>
			<td> <span style="color:#00FF00;background:black;">(0 1 0)</span> </td>
			<td> <span style="color:#00FF00;background:white;">(0 1 0)</span> </td>
		</tr>
		<tr>
			<td> 4 Hz</td>
			<td> <span style="color:#FFFF00;background:black;">(1 1 0)</span> </td>
			<td> <span style="color:#CCCC00;background:white;">(0.8 0.8 0)</span> </td>
		</tr>
		<tr>
			<td> 6 Hz</td>
			<td> <span style="color:#FF7F00;background:black;">(1 0.5 0)</span> </td>
			<td> <span style="color:#D26600;background:white;">(0.9 0.4 0)</span> </td>
		</tr>
		<tr>
			<td> 8 Hz</td>
			<td> <span style="color:#FF0000;background:black;">(1 0 0)</span> </td>
			<td> <span style="color:#FF0000;background:white;">(1 0 0)</span> </td>
		</tr>
		<tr>
			<td> 10 Hz</td>
			<td> <span style="color:#FF007F;background:black;">(1 0 0.5)</span> </td>
			<td> <span style="color:#FF007F;background:white;">(1 0 0.5)</span> </td>
		</tr>
		<tr>
			<td> 12 Hz</td>
			<td> <span style="color:#FF00FF;background:black;">(1 0 1)</span> </td>
			<td> <span style="color:#FF00FF;background:white;">(1 0 1)</span> </td>
		</tr>
		<tr>
			<td> 14 Hz</td>
			<td> <span style="color:#7F00E6;background:black;">(0.5 0 0.9)</span> </td>
			<td> <span style="color:#7F00FF;background:white;">(0.5 0 1)</span> </td>
		</tr>
		<tr>
			<td> 16 Hz</td>
			<td> <span style="color:#3333FF;background:black;">(0.2 0.2 1)</span> </td>
			<td> <span style="color:#0000FF;background:white;">(0 0 1)</span> </td>
		</tr>
		<tr>
			<td> 18 Hz</td>
			<td> <span style="color:#66667F;background:black;">(0.4 0.4 0.5)</span> </td>
			<td> <span style="color:#00007F;background:white;">(0 0 0.5)</span> </td>
		</tr>
		<tr>
			<td> 20 Hz</td>
			<td> <span style="color:#FFFFFF;background:black;">(1 1 1)</span> </td>
			<td> <span style="color:#000000;background:white;">(0 0 0)</span> </td>
		</tr>
	</table></div>
    </div>
 
Decoding code

```cpp
double colormapWhiteBackground[] = {0, 1, 1, 0, 1, 0, 0.8, 0.8, 0, 0.9, 0.4, 0, 1, 0, 0, 1, 0, 0.5, 1, 0, 1, 0.5, 0, 1, 0, 0, 1, 0, 0, 0.5, 0, 0, 0,}; // for white background
double colormap[] = {0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0.5, 0, 1, 0, 0, 1, 0, 0.5, 1, 0, 1, 0.5, 0, 0.9, 0.2, 0.2, 1, 0.4, 0.4, 0.5, 1, 1, 1,}; // for black background
   
const double Jcoupling = 7.1 ; // Hz
const double JcouplingAbs = abs(Jcoupling) ; // Hz
const int baseColorInt = floor(JcouplingAbs / 2.0)); // -20 - 20.0 ->  0 - 9 
if (baseColorInt > 9) baseColorInt = 9; // baseColorInt 0 - 9
float adjust = (JcouplingAbs - 2 * baseColorInt) / 2.0; // normalized diff (0-1)
if (adjust > 1.0) adjust = 1.0; // adjust 0 - 1.0
baseColorIndex =  3 * baseColorInt; // 3 because RGB
// the loop is language dependent, lets drop it...
curColor[0] = colormap[baseColorIndex + 0] + adjust * (colormap[baseColorIndex + 3 + 0] - colormap[baseColorIndex + 0]);
curColor[1] = colormap[baseColorIndex + 1] + adjust * (colormap[baseColorIndex + 3 + 1] - colormap[baseColorIndex + 1]);
curColor[2] = colormap[baseColorIndex + 2] + adjust * (colormap[baseColorIndex + 3 + 2] - colormap[baseColorIndex + 2]);

const bool negExpVal = (expVal < 0.0); // used to change line type for negative values.                      
```
