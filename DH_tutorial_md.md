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

- Gabor, D. (1949). Microscopy by reconstructed wave-fronts. *Proceedings of the Royal Society of London. Series A. Mathematical and Physical Sciences*, *197*(1051), 454–487. https://doi.org/10.1098/rspa.1949.0075

<img src="DH_tutorial_md.assets/image-20220426134139308.png" alt="image-20220426134139308" style="zoom: 25%;" />

##### Leigth & Upatnieks

- Leith, E. N., & Upatnieks, J. (1964). Wavefront Reconstruction with Diffused Illumination and Three-Dimensional Objects. *J. Opt. Soc. Am.*, *54*(11), 1295–1301. https://doi.org/10.1364/JOSA.54.001295

<img src="DH_tutorial_md.assets/image-20220426135144501.png" alt="image-20220426135144501" style="zoom: 80%;" />

##### JW Goodman

- Goodman, J. W., & Lawrence, R. W. (1967). DIGITAL IMAGE FORMATION FROM ELECTRONICALLY DETECTED HOLOGRAMS. *Applied Physics Letters*, *11*(3), 77–79. https://doi.org/10.1063/1.1755043

<img src="DH_tutorial_md.assets/image-20220426135625638.png" alt="image-20220426135625638" style="zoom: 25%;" />

##### Jueptner & Schnars

- Schnars, U., & Jüptner, W. (1994). Direct recording of holograms by a CCD target and numerical reconstruction. *Appl. Opt.*, *33*(2), 179–181. https://doi.org/10.1364/AO.33.000179

<img src="DH_tutorial_md.assets/image-20220426140019172.png" alt="image-20220426140019172" style="zoom:50%;" />

##### Depeursinge

- Cuche, E., Bevilacqua, F., & Depeursinge, C. (1999). Digital holography for quantitative phase-contrast imaging. *Opt. Lett.*, *24*(5), 291–293. https://doi.org/10.1364/OL.24.000291

<img src="DH_tutorial_md.assets/image-20220426140050211.png" alt="image-20220426140050211" style="zoom:50%;" />



### basic theory of DH

##### holographic terms

<img src="DH_tutorial_md.assets/image-20220415152931893.png" alt="image-20220415152931893" style="zoom: 67%;" />

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

- FTM:
  $$
  Z_{\min} = \frac{X_0^2}{N\lambda}; \qquad\qquad Z_{\max} = \frac{X_0^2}{2\lambda}
  $$



##### sample Python code for AS diffraction

- AS_diffraction.py
- input abs & phs
- angular spectrum
- output abs & phs



```
def asdiffract(EE):    
    xx, yy = meshgrid(-ax/2:dx:ax/2-dx, -ay/2:dy:ay/2-dy)
    k = 2*pi/wlen
    dkx, dky = 2*pi/ax, 2*pi/ay
    akx, aky = 2*pi/dx, 2*pi/dy
    kxx, kyy = meshgrid(-akx/2:dkx:akx/2-dkx, -aky/2:dky:aky/2-dky)
    
    FF = fftshift(fft(EE))    
    GG = exp(1j*z*sqrt(k**2 - kxx**2 - kyy**2))    
    HH = ifft(ifftshift(FF * GG))
    
    % EE: [xx,yy]
    % FF, GG: [kxx, kyy]
    % HH: [xx, yy]
    return HH
```



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

<img src="DH_tutorial_md.assets/image-20220426154854457.png" alt="image-20220426154854457" style="zoom:50%;" />

<img src="DH_tutorial_md.assets/image-20220426154916787.png" alt="image-20220426154916787" style="zoom:50%;" />

- imaging characteristics

##### phase-shifting digital holography

- optical configuration

<img src="DH_tutorial_md.assets/image-20220426155721421.png" alt="image-20220426155721421" style="zoom: 33%;" />

- imaging characteristics

<img src="DH_tutorial_md.assets/image-20220426155750402.png" alt="image-20220426155750402" style="zoom:50%;" />


$$
E_O(x,y) = \mathcal{E}_O(x,y)\exp[i\Phi(x,y)] \\
E_R = \mathcal{E}_R e^{i\alpha_n} \\
\alpha_n = \frac{2\pi}{N}n \qquad n=1,2,3,\cdots,N \\
I_n = |E_R + E_O|^2 = \mathcal{E}_R^2 + \mathcal{E}_O^2 + \mathcal{E}_R\mathcal{E}_O e^{i(\alpha_n-\Phi)} + \mathcal{E}_R\mathcal{E}_O e^{i(-\alpha_n+\Phi)} \\
S=\frac{1}{N}\sum_{n=1}^N I_n e^{i\alpha_n} = \frac{1}{N}\left\{\left[\mathcal{E}_R^2 + \mathcal{E}_O^2 \right]\sum_n e^{i\alpha_n} + \mathcal{E}_R\mathcal{E}_O e^{-i\Phi}\sum_n e^{2i\alpha_n} + \mathcal{E}_R\mathcal{E}_O e^{i\Phi}N \right\} \\
= \mathcal{E}_R\mathcal{E}_O(x,y)\exp[i\Phi(x,y)] \\
E_O(x,y) = \frac{1}{N\mathcal E_R}\sum_{n=1}^N I_n e^{i\alpha_n}
$$

- for $N=4$:

$$
\Phi(x,y) = \atan\frac{I_1 - I_3}{I_2 - I_4}
$$



##### sample PSDH.py code

- python code
- frames
- output abs & phs



```
def psdh(HH):
	ny, nx, nph = shape(HH)
	EE = zeros(ny,nx)
	for n in range(nph):
		EE += HH[:,:,n] * exp(1i*n*2*pi/nph)
    EE = EE/nph
    return EE
```





##### off-axis holography

![image-20220416170733456](DH_tutorial_md.assets/image-20220416170733456.png)
$$
B = \frac{2}{2+3\sqrt{2}}K = \beta K \qquad \beta=0.32 \\
K_0 = \frac{3}{2\sqrt{2}}B = \frac{3}{2\sqrt{2}+6} K = \gamma K \qquad \gamma=0.34 \qquad \sqrt{2}\,\gamma = 0.48
$$


- optical configuration

<img src="DH_tutorial_md.assets/image-20220426154947369.png" alt="image-20220426154947369" style="zoom:50%;" />


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



## WSQPM

##### WSQPM theory







##### WSQPM process

##### sample python code

##### WSQPM examples: mkkim

##### WSQPM examples: survey



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



|        | wavelength | angle |      |      |
| ------ | ---------- | ----- | ---- | ---- |
| 1W QPM | QPM        |       |      |      |
| 2W QPM | 2WOPU      | 2AOPU |      |      |
| MW QPM | MWOPU      | MAOPU |      |      |
| WS QPM | WSOPU      | ASOPU |      |      |
| WS DIH | WSDIH      | ASDIH |      |      |
|        |            |       |      |      |



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



##### 1WQPM

- Mann, C. J., Yu, L., Lo, C.-M., & Kim, M. K. (2005). High-resolution quantitative phase-contrast microscopy by digital holography. *Optics Express*, *13*(22), 8693. https://doi.org/10.1364/opex.13.008693



##### 2WQPM

- Gass, J., Dakoff, A., & Kim, M. K. (2003). Phase imaging without 2π ambiguity by multiwavelength digital holography. *Optics Letters*, *28*(13), 1141. https://doi.org/10.1364/ol.28.001141





##### MWQPM

- Kim, M. K. (2022). Phase microscopy and surface profilometry by digital holography. *Light: Advanced Manufacturing*, *3*(1), 1. https://doi.org/10.37188/lam.2022.019
- Wagner, C., Osten, W. & Seebacher, S. Direct shape measurement bydigital  wavefront  reconstruction  and  multi-wavelength  contouring.Optical Engineering39, 79-85 (2000).





##### WSQPM

- 





##### WSDIH

- Kim, M. K. (1999). Wavelength-scanning digital interference holography for optical section imaging. *Optics Letters*, *24*(23), 1693. https://doi.org/10.1364/ol.24.001693





##### MAQPM

- Kim, M. K. (2022). Phase microscopy and surface profilometry by digital holography. *Light: Advanced Manufacturing*, *3*(1), 1. https://doi.org/10.37188/lam.2022.019





##### ASQPM

- Psota,  P.,  et  al.  Multiple  angle  digital  holography  for  the  shapemeasurement of the unpainted tympanic membrane. Optics  Express28, 24614-24628 (2020).
- Martinez-Carranza,  J.,  et  al.  Multi-incidence  digital  holographicprofilometry  with  high  axial  resolution  and  enlarged  measurementrange. Optics Express28, 8185-8199 (2020)





##### ASDIH

- Je on, Y. & Hong, C. K. Optical section imaging of the tilted planes byillumination-angle-scanning  digital  interference  holography. AppliedOptics49, 5110-5116 (2010).
- Do ng, J., J ia, S. H. & Jiang, C. Surface shape measurement by multi-illumination   lensless   Fourier   transform   digital   holographicinterferometry. Optics Communications402, 91-96 (2017).







------

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
- [ ] beta scan
- [ ] diffraction
- [ ] MWDH biblio



























