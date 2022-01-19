# Color map for J coupling 

This color map was designed for [J-graphs](https://nmredatainitiative.github.io/J-graph/) and other color-coded representation of NMR J(H,H) ranging from 0 to 20 Hz.

It was chosen order to provide a large color contrast for values that are particularily significant (small, about 7.0 and about 12 Hz).

<table>
		<tr>
			<th>J </th>
			<th>Black background</th>
			<th>White background</th>
		</tr>
		<tr>
			<td>Hz</td>
			<td>RGB (0-1)</td>
			<td>RGB (0-1)</td>
		</tr>
		<tr>
			<td> 0</td>
			<td> <span style="color:#00FFFF;background:black;">(0 1 1)</span> </td>
			<td> <span style="color:#00FFFF;background:white;">(0 1 1)</span> </td>
		</tr>
		<tr>
			<td> 2</td>
			<td> <span style="color:#00FF00;background:black;">(0 1 0)</span> </td>
			<td> <span style="color:#00FF00;background:white;">(0 1 0)</span> </td>
		</tr>
		<tr>
			<td> 4</td>
			<td> <span style="color:#FFFF00;background:black;">(1 1 0)</span> </td>
			<td> <span style="color:#CCCC00;background:white;">(0.8 0.8 0)</span> </td>
		</tr>
		<tr>
			<td> 6</td>
			<td> <span style="color:#FF7F00;background:black;">(1 0.5 0)</span> </td>
			<td> <span style="color:#D26600;background:white;">(0.9 0.4 0)</span> </td>
		</tr>
		<tr>
			<td> 8</td>
			<td> <span style="color:#FF0000;background:black;">(1 0 0)</span> </td>
			<td> <span style="color:#FF0000;background:white;">(1 0 0)</span> </td>
		</tr>
		<tr>
			<td> 10</td>
			<td> <span style="color:#FF007F;background:black;">(1 0 0.5)</span> </td>
			<td> <span style="color:#FF007F;background:white;">(1 0 0.5)</span> </td>
		</tr>
		<tr>
			<td> 12</td>
			<td> <span style="color:#FF00FF;background:black;">(1 0 1)</span> </td>
			<td> <span style="color:#FF00FF;background:white;">(1 0 1)</span> </td>
		</tr>
		<tr>
			<td> 14</td>
			<td> <span style="color:#7F00E6;background:black;">(0.5 0 0.9)</span> </td>
			<td> <span style="color:#7F00FF;background:white;">(0.5 0 1)</span> </td>
		</tr>
		<tr>
			<td> 16</td>
			<td> <span style="color:#3333FF;background:black;">(0.2 0.2 1)</span> </td>
			<td> <span style="color:#0000FF;background:white;">(0 0 1)</span> </td>
		</tr>
		<tr>
			<td> 18</td>
			<td> <span style="color:#66667F;background:black;">(0.4 0.4 0.5)</span> </td>
			<td> <span style="color:#00007F;background:white;">(0 0 0.5)</span> </td>
		</tr>
		<tr>
			<td> 20</td>
			<td> <span style="color:#FFFFFF;background:black;">(1 1 1)</span> </td>
			<td> <span style="color:#000000;background:white;">(0 0 0)</span> </td>
		</tr>
	</table>

Convert J value into (R, G, B) values (0 - 1).

```cpp
// input
const double Jcoupling = 7.1 ; // Hz

// Color maps. First color for 0 Hz, second color for 2 Hz, etc. up to 20 Hz
const double colormapWhiteBackground[] = {0, 1, 1, 0, 1, 0, 0.8, 0.8, 0, 0.9, 0.4, 0, 1, 0, 0, 1, 0, 0.5, 1, 0, 1, 0.5, 0, 1, 0, 0, 1, 0, 0, 0.5, 0, 0, 0,}; // for white background
const double colormap[] = {0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0.5, 0, 1, 0, 0, 1, 0, 0.5, 1, 0, 1, 0.5, 0, 0.9, 0.2, 0.2, 1, 0.4, 0.4, 0.5, 1, 1, 1,}; // for black background
   
const double JcouplingAbs = abs(Jcoupling) ; // Hz
int baseColorInt = floor(JcouplingAbs / 2.0); // -20 - 20.0 ->  0 - 9 
if (baseColorInt > 9) baseColorInt = 9; // baseColorInt 0 - 9
float adjust = (JcouplingAbs - 2 * baseColorInt) / 2.0; // normalized diff (0-1) for 2 Hz
if (adjust > 1.0) adjust = 1.0; // adjust 0 - 1.0
const int baseColorIndex =  3 * baseColorInt; // 3 because RGB

// Output
double curColor[] = {0, 0, 0}; // RGB
// the loop is language dependent, lets drop it...
curColor[0] = colormap[baseColorIndex + 0] + adjust * (colormap[baseColorIndex + 3 + 0] - colormap[baseColorIndex + 0]);
curColor[1] = colormap[baseColorIndex + 1] + adjust * (colormap[baseColorIndex + 3 + 1] - colormap[baseColorIndex + 1]);
curColor[2] = colormap[baseColorIndex + 2] + adjust * (colormap[baseColorIndex + 3 + 2] - colormap[baseColorIndex + 2]);

const bool negExpVal = (Jcoupling < 0.0); // used to change line type for negative values.                   
```

Please make pull requests or raise issue to send us your code in other languages!
