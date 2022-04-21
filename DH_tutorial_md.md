**Optica: Digital Holography and Three-Dimensional Imaging**

**Cambridge University, Cambridge, UK**



# Multi-Wavelength Techniques in Digital Holography: Tutorial



**Myung K Kim**

Dept of Physics, University of South Florida, Tampa, FL 33620 USA

August 2022



### abstract

Basic principles and techniques will be described for multi-wavelength or multi-illumination-angle mehtods for extending capabilities of digital holography for surface profilometry by optical phase unwrapping and topography/tomography by synthesized optical coherence



- intro for new researchers & students
- details of theory
- details of experiment
- details of numerical methods
- highlight my research
- survey others research



### acknowledgement





## Holography Intro

### beginning

##### Gabor

##### Leigth & Upatnieks

##### JW Goodman

##### Jueptner & Schnars

##### Depeursinge



### basic theory of DH

##### holographic terms

<img src="DH_tutorial_md.assets/image-20220415152931893.png" alt="image-20220415152931893" style="zoom:50%;" />

- hologram recording

$$
I = |E_R + E_O|^2 = |E_R|^2 + |E_O|^2 +E_R^*E_O + E_RE_O^*
$$

- hologram reconstruction

$$
E = E'_RI = E'_R|E_R+E_O|^2 \\ 
=E'_R|E_R|^2 + E'_R|E_O|^2 + E'_RE_R^*E_O + E'_RE_RE_O^*
$$



##### holography of elementray waves

- holography of plane waves
- holography of spherical waves

<img src="DH_tutorial_md.assets/image-20220415152849132.png" alt="image-20220415152849132" style="zoom:50%;" />

##### diffraction from a 2D aperture

<img src="DH_tutorial_md.assets/image-20220415162604622.png" alt="image-20220415162604622" style="zoom: 33%;" />


$$
E(x,y;z) = -\frac{ik}{2\pi} \iint_{\Sigma_0} dx_0dy_0\,E_0(x_0,y_0)\frac{\exp(ikr)}{r} \\
\approx -\frac{ik}{2\pi z} \iint_{\Sigma_0} dx_0dy_0\,E_0(x_0,y_0)\exp\left[ik\sqrt{(x-x_0)^2 + (y-y_0)^2 + z^2 }\right] \\
= E_0 \odot S_H \\
\\
\textbf{spherical wavefront} \qquad S_H(x,y;z) = - \frac{ik}{2\pi z} \exp\left[ik\sqrt{x^2+y^2+z^2}\right]
$$


##### Fresnel transform method

$$
r \approx z + \frac{x^2+y^2}{2z} \\
E(x,y) = - \frac{ik}{2\pi z} \exp\left[ikz + \frac{ik}{2z} (x^2+y^2)\right] \iint dx_0\,dy_0E_0(x_0,y_0)\exp\left[\frac{ik}{2z}(x_0^2+y_0^2)\right]\exp\left[-\frac{ik}{z}(xx_0+yy_0)\right] \\
=\exp\left[\frac{ik}{2z}(x^2+y^2)\right]F\{E_0S_F\} \\
\textbf{parabolic wave front} \qquad S_F(x,y;z) = -\frac{ik}{2\pi z}\exp\left[ikz + \frac{ik}{2z}(x^2+y^2)\right]
$$



##### propagation of angular spectrum



<img src="DH_tutorial_md.assets/image-20220415153149971.png" alt="image-20220415153149971" style="zoom:33%;" />

- angular spectrum of input wave: plane wave components

$$
A_0(k_x,k_y) = F\left\{E_0(x_0,y_0)\right\}\left[k_x,k_y\right] \\
=\frac{1}{2\pi}\iint_{\Sigma_0} dx_0 dy_0 E_0(x_0,y_0) \exp\left[-i(k_x x_0 + k_y y_0)\right]
$$

- output wave is the sum of propagated input plane wave components

$$
E(x,y,z) = F^{-1}\left\{A_0(k_x,k_y) \exp[ik_z z]\right\}[x,y] \\
= F^{-1}\left\{F\{E_0\}\exp\left[i\sqrt{k^2 - k_x^2 - k_y^2}\ z\right]\right\} \\
k_z = \sqrt{k^2 - k_x^2 - k_y^2} \qquad \left[ k_x^2 + k_y^2 \le k^2 \right]
$$



##### FFT: fast Fourier transform

<img src="DH_tutorial_md.assets/image-20220416111943805.png" alt="image-20220416111943805" style="zoom:50%;" />
$$
F\left\{f(x,y)\right\}[k_x,k_y] = \frac{1}{2\pi}\iint dx\,dy\,f(x,y)\exp\left[-i(k_x x + k_yy)\right] = F(k_x,k_y) \\
F^{-1}\left\{F(k_x,k_y)\right\}[x,y] = \frac{1}{2\pi}\iint dk_x\,dk_y\,F(k_x,k_y)\exp\left[+i(k_x x + k_yy)\right] = f(x,y) \\
\\
K_x = 2\pi/dx \qquad dk_x = 2\pi/A_x = K_x/N_x \\
K_y = 2\pi/dy \qquad dk_y = 2\pi/A_y = K_y/N_y
$$

- $K_x/k=\lambda/dx$: maximum slope of wavefront before violating Nyquist
- $dk/k = \lambda/A_x$: minimum slope of wavefront to record one cycle over the frame size $A_x$ 



##### comparison of methods

- HCM vs ASM

<img src="DH_tutorial_md.assets/image-20220415160427601.png" alt="image-20220415160427601" style="zoom: 33%;" />

- FTM vs HCM vs ASM

<img src="DH_tutorial_md.assets/image-20220415160459990.png" alt="image-20220415160459990" style="zoom: 50%;" />



##### sample Python code for AS diffraction

- AS_diffraction.py
- input abs & phs
- angular spectrum
- output abs & phs



## Digital Holography Systems

##### DHM apparatus - reflection

- optical configuration

<img src="DH_tutorial_md.assets/image-20220416172051992.png" alt="image-20220416172051992"  />

<img src="DH_tutorial_md.assets/image-20220416172121347.png" alt="image-20220416172121347" style="zoom: 80%;" />



##### DHM apparatus - transmission

- optical configuration

<img src="DH_tutorial_md.assets/image-20220416171646079.png" alt="image-20220416171646079" style="zoom:50%;" />



<img src="DH_tutorial_md.assets/image-20220416171658927.png" alt="image-20220416171658927" style="zoom: 50%;" />



##### Gabor in-line holography

- optical configuration
- imaging characteristics

##### phase-shifting digital holography

- optical configuration
- imaging characteristics

##### sample PSDH.py code

- python code
- frames
- output abs & phs

##### off-axis holography

![image-20220416170733456](DH_tutorial_md.assets/image-20220416170733456.png)
$$
B = \frac{2}{2+3\sqrt{2}}K = \beta K \qquad \beta=0.32 \\
K_0 = \frac{3}{2\sqrt{2}}B = \frac{3}{2\sqrt{2}+6} K = \gamma K \qquad \gamma=0.34 \qquad \sqrt{2}\,\gamma = 0.48
$$


- optical configuration
- imaging characteristics

##### sample OXDH.py code

- python code
- input camera frame
- angular spectrum
- output abs & phs

##### DHM examples: survey

<img src="DH_tutorial_md.assets/image-20220416215324683.png" alt="image-20220416215324683"  />



- **Figure 4.** DHM phase shift image of human [red blood cells](https://en.wikipedia.org/wiki/Red_blood_cells).

<img src="DH_tutorial_md.assets/220px-DHM_image_of_human_red_blood_cells.jpg" alt="img" style="zoom:150%;" />



- **Figure 5.** Time-lapse of unstained, dividing and migrating cells. 

<img src="DH_tutorial_md.assets/DHM-CellTimeLapse.gif" alt="img" style="zoom:150%;" />





## Multi-Wavelength Background

##### multi-wavelength: motivation

##### multi-wavelength: history

##### wavelength-scanning: history



## 2W DHQPM

##### QPM with single wavelength

$$
E(x,y) = a(x,y)\cdot\exp[i\Phi(x,y)] \\
a \ //\ b \quad \equiv \textrm{mod}\left(a+\frac{b}{2},\ b\right)-\frac{b}{2} \qquad \in \left[-\frac{b}{2}, \frac{b}{2}\right]\\
\Phi(x,y) = \left[ 2\pi\ \frac{Z(x,y)}{\lambda} \right] \ //\ 2\pi \qquad \in [-\pi,\pi] \\
Z_\lambda(x,y) = \lambda\ \frac{\Phi(x,y)}{2\pi} \qquad \in \left[-\frac{\lambda}{2}, \frac{\lambda}{2}\right]
$$

- 1WQPM graphs



##### 2WOPU

$$
E_n(x,y) = a_n(x,y)\cdot\exp[i\Phi_n(x,y)] \\
E_{12}(x,y) = E_1\cdot E_2^* = a_{12}\cdot\exp[i\Phi_{12}(x,y)]\\
\Phi_{12}(x,y) = (\Phi_1 - \Phi_2) \ //\ 2\pi = \left[ 2\pi\ \frac{Z(x,y)}{\Lambda_{12}} \right]\ //\ 2\pi \qquad \in [-\pi,\pi] \\
\frac{1}{\Lambda_{12}} = \frac{1}{\lambda_1} - \frac{1}{\lambda_2} \qquad\rightarrow\qquad \Lambda_{12} = -\frac{\lambda_1 \lambda_2}{\lambda_1 - \lambda_2} \\
Z_{12}(x,y) = \Lambda_{12}\cdot\frac{\Phi_{12}(x,y)}{2\pi} \qquad \in\left[-\frac{\Lambda_{12}}{2}, \frac{\Lambda_{12}}{2} \right] \\
\frac{\Lambda}{\lambda} = \frac{\lambda}{\Delta\lambda}
$$



##### 2WOPU process

##### sample python code

##### 2WOPU examples: mkkim

##### 2WOPU examples: survey



## MW DHQPM

##### noise in 2WOPU

$$
\delta\Phi_n = 2\pi\epsilon \\
\delta Z_n = \lambda_n\ \frac{\delta\Phi_n}{2\pi} = \lambda_n\epsilon \\
\delta\Phi_{12} = \sqrt{2}\ 2\pi\ \epsilon \\
\delta Z_{12} = \sqrt{2}\ \Lambda_{12}\ \epsilon \\
\frac{\delta Z_{12}}{\delta Z_n} = \frac{\sqrt{2}\ \Lambda_{12}}{\lambda_n}
$$



##### noise reduction by 3WOPU

$$
Z_{12\_3}(x,y) = \textrm{round}\left[\frac{Z_{12}(x,y)}{\Lambda_{13}}\right]\ \Lambda_{13} + Z_{13}(x,y) \\
Z_{12\_3} + \delta Z_{12\_3} = \textrm{round}\left[\frac{Z_{12} + \delta Z_{12}}{\Lambda_{13}} \right] \  \Lambda_{13} + (Z_{13} + \delta \Z_{13})  \\
\delta Z_{12\_3} = \Delta\cdot \Lambda_{13} + \delta Z_{13} = \Delta\cdot\Lambda_{13} + \sqrt{2}\ \Lambda_{13}\ \epsilon \\
$$

- $\Delta\cdot\Lambda_{13}$: 		spikes of height $\Lambda_{13}$ scattered near $\textrm{round()}$ boundaries within $\delta Z_{12}$ 
- require:

$$
\frac{\delta Z_{12}}{\Lambda_{13}} = \sqrt{2}\ \epsilon\ \frac{\Lambda_{12}}{\Lambda_{13}} \ll 1 \\
\alpha = \frac{\Lambda_{13}}{\Lambda_{12}} \gg \sqrt{2}\ \epsilon
$$

- despiking:

$$
Z_{12\_3} - Z_{12} = s\ \Delta Z \\
\bar{Z}_{12\_3} = Z_{12\_3} - s\ \Lambda_{13}\cdot\left(\Delta Z \gg \delta Z_{13}\right)\  \\
\delta\bar{Z}_{12\_3} = \delta Z_{13} = \sqrt{2}\ \Lambda_{13}\ \epsilon
$$



##### MWOPU

$$
\{\lambda_n\} = \lambda_1,\ \lambda_2,\ \lambda_3,\ \cdots \\
E_n(x,y) = a_n(x,y)\cdot\exp[i\Phi_n(x,y)] \\
n \ge 2:\quad E_{1n}(x,y) = E_1\cdot E_n^* = a_{1n}(x,y)\cdot\exp[i\Phi_{1n}(x,y)] \\
\Phi_{1n}(x,y) = (\Phi_1 - \Phi_2)//2\pi = \left[ 2\pi\ \frac{Z(x,y)}{\Lambda_{1n}} \right]\ //\ 2\pi \\
\Lambda_{1n} = -\frac{\lambda_1\lambda_n}{\lambda_1 - \lambda_n} \\
Z_{1n}(x,y) = \Lambda_{1n}\ \frac{\Phi_{1n}(x,y)}{2\pi} \\
\delta Z_{1n} = \sqrt{2}\ \Lambda_{1n}\ \epsilon \\
n \ge 3:\quad Z_{12\_n}(x,y) = \textrm{round}\left[\frac{Z_{12\_(n-1)}(x,y)}{\Lambda_{1n}} \right]\cdot\Lambda_{1n} + Z_{1n}(x,y) \\
\delta Z_{12\_n} = \Delta\cdot\Lambda_{1n} + \delta Z_{1n} \\
Z_{12\_n} - Z_{12\_(n-1)} = s\ \Delta Z \\
\bar{Z}_{12\_n} = Z_{12\_n} - s\ \Lambda_{1n}\cdot(\Delta Z \gg \delta Z_{1n}) \\
\delta\bar{Z}_{12\_n} = \delta Z_{1n} = \sqrt{2}\cdot\Lambda_{1n}\epsilon
$$





##### MWOPU process

##### sample python code

##### MWOPU examples: mkkim

##### MWOPU examples: survey



## WSDIH

##### theory of WSDIH

##### WSDIH process

##### sample python code

##### WSDIH examples: mkkim

##### WSDIH examples: survey



## Multi-Wavelength Generation

##### discrete lasers

##### tunable lsers

##### index tuning

##### angle scanning



## MA DHQPM

##### theory of MAOPU

##### MAOPU process

##### sample python code

##### MAOPU examples: mkkim

##### MAOPU examples: survey



## ASDIH

##### theory of ASDIH

##### ASDIH process

##### sample python code

##### ASDIH examples: mkkim

##### ASDIH examples: survey



## Further Development







## References



##### DHM examples: survey



##### multi-wavelength: history



##### wavelength-scanning: history



##### 2WOPU examples: survey



##### MWOPU examples: survey



##### WSDIH examples: survey



##### MAOPU examples: survey



##### ASDIH examples: survey









## todolist

- [ ] theories
- [ ] 







































