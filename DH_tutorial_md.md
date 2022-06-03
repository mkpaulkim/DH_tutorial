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

> - lensless imaging for aberrations in electron microscope
> - optical demonstration experiment

##### Leigth & Upatnieks

- Leith, E. N., & Upatnieks, J. (1964). Wavefront Reconstruction with Diffused Illumination and Three-Dimensional Objects. *J. Opt. Soc. Am.*, *54*(11), 1295–1301. https://doi.org/10.1364/JOSA.54.001295

<img src="DH_tutorial_md.assets/image-20220426135144501.png" alt="image-20220426135144501" style="zoom: 80%;" />

> - laser: sources of long coherence
> - separation of holographic terms

##### JW Goodman

- Goodman, J. W., & Lawrence, R. W. (1967). DIGITAL IMAGE FORMATION FROM ELECTRONICALLY DETECTED HOLOGRAMS. *Applied Physics Letters*, *11*(3), 77–79. https://doi.org/10.1063/1.1755043

<img src="DH_tutorial_md.assets/image-20220426135625638.png" alt="image-20220426135625638" style="zoom: 25%;" />

> - Fourier hologram 256 x 256 pixels, 5 minutes of computation on PDP-6

##### Jueptner & Schnars

- Schnars, U., & Jüptner, W. (1994). Direct recording of holograms by a CCD target and numerical reconstruction. *Appl. Opt.*, *33*(2), 179–181. https://doi.org/10.1364/AO.33.000179

<img src="DH_tutorial_md.assets/image-20220426140019172.png" alt="image-20220426140019172" style="zoom:50%;" />

> - CCD recording  and numerical reconstruction of  Fresnel off-axis hologram

##### Depeursinge

- Cuche, E., Bevilacqua, F., & Depeursinge, C. (1999). Digital holography for quantitative phase-contrast imaging. *Opt. Lett.*, *24*(5), 291–293. https://doi.org/10.1364/OL.24.000291

<img src="DH_tutorial_md.assets/image-20220426140050211.png" alt="image-20220426140050211" style="zoom:50%;" />

> - reconstruction of complex optical field: amplitude and phase profiles



### basic theory of DH

##### holographic terms

<img src="DH_tutorial_md.assets/image-20220415152931893.png" alt="image-20220415152931893" style="zoom: 67%;" />

- hologram recording

$$
I = |E_R + E_O|^2 = |E_R|^2 + |E_O|^2 +E_R^*E_O + E_RE_O^*
$$

- hologram reconstruction

$$
E'_RI = E'_R|E_R+E_O|^2 \\ 
=E'_R|E_R|^2 + E'_R|E_O|^2 + E'_RE_R^*E_O + E'_RE_RE_O^*
$$



##### holography of elementray waves

- holography of plane waves
- holography of spherical waves

<img src="DH_tutorial_md.assets/image-20220415152849132.png" alt="image-20220415152849132" style="zoom:50%;" />

##### diffraction from a 2D aperture: Huygens convoluton method

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
=\exp\left[\frac{ik}{2z}(x^2+y^2)\right]\mathscr F\{E_0S_F\} \\
\textbf{parabolic wave front} \qquad S_F(x,y;z) = -\frac{ik}{2\pi z}\exp\left[ikz + \frac{ik}{2z}(x^2+y^2)\right]
$$



##### propagation of angular spectrum (plane wave decomposition)



<img src="DH_tutorial_md.assets/image-20220415153149971.png" alt="image-20220415153149971" style="zoom:33%;" />

- angular spectrum of input wave: plane wave components

$$
A_0(k_x,k_y) = \mathscr F\left\{E_0(x_0,y_0)\right\}\left[k_x,k_y\right] \\
=\frac{1}{2\pi}\iint_{\Sigma_0} dx_0 dy_0 E_0(x_0,y_0) \exp\left[-i(k_x x_0 + k_y y_0)\right]
$$

- output wave is the sum of propagated input plane wave components

$$
E(x,y,z) = \mathscr F^{-1}\left\{A_0(k_x,k_y) \exp[ik_z z]\right\}[x,y] \\
= \mathscr F^{-1}\left\{\mathscr F\{E_0\}\exp\left[i\sqrt{k^2 - k_x^2 - k_y^2}\ z\right]\right\} \\
k_z = \sqrt{k^2 - k_x^2 - k_y^2} \qquad \left[ k_x^2 + k_y^2 \le k^2 \right]
$$



##### FFT: fast Fourier transform

<img src="DH_tutorial_md.assets/image-20220416111943805.png" alt="image-20220416111943805" style="zoom:50%;" />
$$
\mathscr F\left\{f(x,y)\right\}[k_x,k_y] = \frac{1}{2\pi}\iint dx\,dy\,f(x,y)\exp\left[-i(k_x x + k_yy)\right] = F(k_x,k_y) \\
\mathscr F^{-1}\left\{F(k_x,k_y)\right\}[x,y] = \frac{1}{2\pi}\iint dk_x\,dk_y\,F(k_x,k_y)\exp\left[+i(k_x x + k_yy)\right] = f(x,y) \\
\\
K_x = 2\pi/dx \qquad dk_x = 2\pi/A_x = K_x/N_x \\
K_y = 2\pi/dy \qquad dk_y = 2\pi/A_y = K_y/N_y
$$

- $K_x/k=\lambda/dx$: maximum slope of wavefront before violating Nyquist
- $dk/k = \lambda/A_x$: minimum slope of wavefront to record one cycle over the frame size $A_x$ 



##### comparison of methods

- HCM vs ASM: propagation of spherical or plane waves

<img src="DH_tutorial_md.assets/image-20220415160427601.png" alt="image-20220415160427601" style="zoom: 33%;" />

- FTM vs HCM vs ASM

> check this figure for z-range

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

<img src="DH_tutorial_md.assets/image-20220427220207929.png" alt="image-20220427220207929" style="zoom:67%;" />



##### DHM apparatus - transmission

- optical configuration

<img src="DH_tutorial_md.assets/image-20220416171646079.png" alt="image-20220416171646079" style="zoom:50%;" />



<img src="DH_tutorial_md.assets/image-20220416171658927.png" alt="image-20220416171658927" style="zoom: 50%;" />



##### Gabor holography

- optical configuration

<img src="DH_tutorial_md.assets/image-20220426154854457.png" alt="image-20220426154854457" style="zoom:50%;" />

> - overlap of dc and twin terms
>
> - particle imaging

##### in-line holography

<img src="DH_tutorial_md.assets/image-20220426154916787.png" alt="image-20220426154916787" style="zoom:50%;" />

- imaging characteristics

> - separate reference beam
> - overlap of dc and twin terms

##### phase-shifting digital holography

- optical configuration

<img src="DH_tutorial_md.assets/image-20220426155721421.png" alt="image-20220426155721421" style="zoom: 33%;" />

> complex optical field from multi-frame acquisition: removal of dc and twin terms

- imaging characteristics

<img src="DH_tutorial_md.assets/image-20220426155750402.png" alt="image-20220426155750402" style="zoom:50%;" />

$$
E_O(x,y) = \mathcal{E}_O(x,y)\exp[i\Phi(x,y)] \\
E_n = \mathcal{E}_R \exp(i2\pi n/N) \\
\alpha_n = \frac{2\pi}{N}n \qquad n=1,2,3,\cdots,N \\
I_n = |E_R + E_O|^2 = \mathcal{E}_R^2 + \mathcal{E}_O^2 + \mathcal{E}_R\mathcal{E}_O e^{i(\alpha_n-\Phi)} + \mathcal{E}_R\mathcal{E}_O e^{i(-\alpha_n+\Phi)} \\
S=\frac{1}{N}\sum_{n=1}^N I_n e^{i\alpha_n} = \frac{1}{N}\left\{\left[\mathcal{E}_R^2 + \mathcal{E}_O^2 \right]\sum_n e^{i\alpha_n} + \mathcal{E}_R\mathcal{E}_O e^{-i\Phi}\sum_n e^{2i\alpha_n} + \mathcal{E}_R\mathcal{E}_O e^{i\Phi}N \right\} \\
= \mathcal{E}_R\mathcal{E}_O(x,y)\exp[i\Phi(x,y)] \\
E_O(x,y) = \frac{1}{N\mathcal E_R}\sum_{n=1}^N I_n \exp(i2\pi n/N)
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
def psdh(HHH):
	ny, nx, nph = shape(HHH)
	EE = zeros(ny,nx)
	for n in range(nph):
		EE += HH[:,:,n] * exp(1j*n*2*pi/nph)
    EE = EE/nph
    return EE
```





##### off-axis holography

- optical configuration

<img src="DH_tutorial_md.assets/image-20220426154947369.png" alt="image-20220426154947369" style="zoom:50%;" />

> - separation of dc and twin terms

- spatial bandwidth

![image-20220416170733456](DH_tutorial_md.assets/image-20220416170733456.png)

> - B: object spatial frequency bandwidth
> - 2B: auto-correlation width
> - K0: carrier frequency by off-axis interference

$$
B = \frac{2}{2+3\sqrt{2}}K = \beta K \qquad \beta=0.32 \\
K_0 = \frac{3}{2\sqrt{2}}B = \frac{3}{2\sqrt{2}+6} K = \gamma K \qquad \gamma=0.34 \qquad \sqrt{2}\,\gamma = 0.48
$$


- imaging characteristics



##### sample OXDH.py code

- python code
- input camera frame
- angular spectrum
- output abs & phs

```
def oxdh(HH, qq):
    xx, yy = meshgrid(-ax/2:dx:ax/2-dx, -ay/2:dy:ay/2-dy)
    k = 2*pi/wlen
    dkx, dky = 2*pi/ax, 2*pi/ay
    akx, aky = 2*pi/dx, 2*pi/dy
    kxx, kyy = meshgrid(-akx/2:dkx:akx/2-dkx, -aky/2:dky:aky/2-dky)
    qx0, qy0, qx, qy = qq	% angular position & width
    kx0, ky0, kx, ky = k*sin(qx0), k*sin(qy0), k*sin(qx), k*sin(qy)    

    FF = fftshift(fft(HH))    
    BB = (((kxx-kx0)/kx)**2 + ((kyy-ky0)/ky)**2) < 1
    FF = FF * BB
    
    EE = ifft(ifftshift(FF)) 
    GG = exp(-1j*(kx0*xx + ky0*yy))
    EE = EE * GG    
    return EE
```



##### DHM examples: survey

- Mann, C. J., Yu, L. F., Lo, C. M., & Kim, M. K. (2005). High-resolution quantitative phase-contrast microscopy by digital holography. *OPTICS EXPRESS*, *13*(22), 8693–8698. https://doi.org/10.1364/OPEX.13.008693

<img src="DH_tutorial_md.assets/image-20220416215324683.png" alt="image-20220416215324683"  />



- Rappaz, B., Barbul, A., Hoffmann, A., Boss, D., Korenstein, R., Depeursinge, C., Magistretti, P. J., & Marquet, P. (2009). Spatial analysis of erythrocyte membrane fluctuations by digital holographic microscopy. *Blood Cells, Molecules, and Diseases*, *42*(3), 228–232. https://doi.org/10.1016/j.bcmd.2009.01.018

<img src="DH_tutorial_md.assets/image-20220427092446148.png" alt="image-20220427092446148" style="zoom: 67%;" />



- **Figure 5.** Time-lapse of unstained, dividing and migrating cells. 

<img src="DHM-CellTimeLapse.gif" alt="img" style="zoom:150%;" />



## Multi-Wavelength Background

##### multi-wavelength: motivation

- QPM with height/thickness range beyond wavelength

##### multi-wavelength: history

- HILDEBRAND, B. P., & HAINES, K. A. (1967). MULTIPLE-WAVELENGTH AND MULTIPLE-SOURCE HOLOGRAPHY APPLIED TO CONTOUR GENERATION. *JOURNAL OF THE OPTICAL SOCIETY OF AMERICA*, *57*(2), 155+. https://doi.org/10.1364/JOSA.57.000155
- Cheng, Y.-Y., & Wyant, J. C. (1984). Two-wavelength phase shifting interferometry. *Appl. Opt.*, *23*(24), 4539–4543. https://doi.org/10.1364/AO.23.004539

##### wavelength-scanning: history



## 2WOPU

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
E_{12}(x,y) \equiv E_1\cdot E_2^* = a_{12}\cdot\exp[i\Phi_{12}(x,y)]\\
\Phi_{12}(x,y) \equiv (\Phi_1 - \Phi_2) \ //\ 2\pi = \left[ 2\pi\ \frac{Z(x,y)}{\Lambda_{12}} \right]\ //\ 2\pi \qquad \in [-\pi,\pi] \\
\frac{1}{\Lambda_{12}} = \frac{1}{\lambda_1} - \frac{1}{\lambda_2} \qquad\rightarrow\qquad \Lambda_{12} = -\frac{\lambda_1 \lambda_2}{\lambda_1 - \lambda_2} \\
Z_{12}(x,y) = \Lambda_{12}\cdot\frac{\Phi_{12}(x,y)}{2\pi} \qquad \in\left[-\frac{\Lambda_{12}}{2}, \frac{\Lambda_{12}}{2} \right] \\
\frac{\Lambda}{\lambda} = \frac{\lambda}{\Delta\lambda}
$$



##### 2WOPU process

<img src="DH_tutorial_md.assets/image-20220427141039405.png" alt="image-20220427141039405" style="zoom:50%;" />

##### sample python code

> def twopu(phi1, ph2, lam1, lam2):
>
> ​	return zz12

##### 2WOPU examples: mkkim

- Khmaladze, A., Kim, M., & Lo, C.-M. (2008). Phase imaging of cells by simultaneous dual-wavelength reflection digital holography. *OPTICS EXPRESS*, *16*(15), 10900–10911. https://doi.org/10.1364/OE.16.010900

<img src="DH_tutorial_md.assets/image-20220427141107699.png" alt="image-20220427141107699" style="zoom:50%;" />

<img src="DH_tutorial_md.assets/image-20220427141311148.png" alt="image-20220427141311148" style="zoom:50%;" />

- Heimbeck, M. S., Kim, M. K., Gregory, D. A., & Everitt, H. O. (2011). Terahertz digital holography using angular spectrum and dual wavelength reconstruction methods. *OPTICS EXPRESS*, *19*(10), 9192–9200. https://doi.org/10.1364/OE.19.009192

<img src="DH_tutorial_md.assets/image-20220427141355546.png" alt="image-20220427141355546"  />

> Fig.  6.  Steps  in  the  reconstruction  of  the  phase  object  using  dual  wavelength  reconstruction: photograph  (a),  holograms  at  680  and  725  GHz  (b-c),  amplitude  reconstructions  (d-e),  phase reconstructions   (f-g),   unwrapped   reconstruction   (h),   cross-section   through   center   of unwrappred reconstruction (i), pseudo 3D perspective of the unwrapped reconstruction (j).

##### 2WOPU examples: survey

- Rinehart, M. T., Shaked, N. T., Jenness, N. J., Clark, R. L., & Wax, A. (2010). Simultaneous two-wavelength transmission quantitative phase microscopy with a color camera. *OPTICS LETTERS*, *35*(15), 2612–2614. https://doi.org/10.1364/OL.35.002612

<img src="DH_tutorial_md.assets/image-20220427143118397.png" alt="image-20220427143118397" style="zoom:50%;" />

<img src="DH_tutorial_md.assets/image-20220427143143483.png" alt="image-20220427143143483" style="zoom: 50%;" />

> Fig. 3. (Color online) Microstructure OPD maps and profiles: (a) 532 nm OPD map after quality-map guided unwrapping, 15 μm lateral scale bar; (b) 532 nm OPD map after two-wavelength unwrapping, 15 μm lateral scale bar; (c) incorrect object height profile, from the dotted line in (a); (d) object height profile from two-wavelength unwrapping, from the dotted line in (b). The quantitative height measurements ob-tained from QPM agree with the SEM images in Fig. 2.

- Lee, Y., Ito, Y., Tahara, T., Inoue, J., Xia, P., Awatsuji, Y., Nishio, K., Ura, S., & Matoba, O. (2014). Single-shot dual-wavelength phase unwrapping in parallel phase-shifting digital holography. *OPTICS LETTERS*, *39*(8), 2374–2377. https://doi.org/10.1364/OL.39.002374

<img src="DH_tutorial_md.assets/image-20220427144722747.png" alt="image-20220427144722747" style="zoom:50%;" />

<img src="DH_tutorial_md.assets/image-20220427144827974.png" alt="image-20220427144827974" style="zoom:50%;" />

> Space bandwidths. Proposed method using (a) parallel two-step phase-shifting interferometry and (b) angular multi-plexing technique.



## MWOPU

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

![image-20220427215653500](DH_tutorial_md.assets/image-20220427215653500.png)

![image-20220427215846786](DH_tutorial_md.assets/image-20220427215846786.png)

![image-20220427215914117](DH_tutorial_md.assets/image-20220427215914117.png)



##### sample python code



##### MWOPU examples: survey

- Wagner, Chr., Osten, W., & Seebacher, S. (2000). Direct shape measurement by digital wavefront reconstruction and multi-wavelength contouring. *Optical Engineering*, *39*(1), 79–85. https://doi.org/10.1117/1.602338

<img src="DH_tutorial_md.assets/image-20220427150423735.png" alt="image-20220427150423735" style="zoom:33%;" />

- Wada, A., Kato, M., & Ishii, Y. (2008). Large step-height measurements using multiple-wavelength holographic interferometry with tunable laser diodes. *JOURNAL OF THE OPTICAL SOCIETY OF AMERICA A-OPTICS IMAGE SCIENCE AND VISION*, *25*(12), 3013–3020. https://doi.org/10.1364/JOSAA.25.003013

<img src="DH_tutorial_md.assets/image-20220427172539858.png" alt="image-20220427172539858" style="zoom: 80%;" />

<img src="DH_tutorial_md.assets/image-20220427172633113.png" alt="image-20220427172633113" style="zoom: 50%;" />

> Object height calculated from $\Delta\phi_6(\Lambda_6=2.5\ \textrm{mm})$. (a) The entire distribution. (b) Plot of the object heights along the black line in panel (a) as a function of lateral position.

- Nardin, G., Colomb, T., Emery, Y., & Moser, C. (2016). Versatile spectral modulation of a broadband source for digital holographic microscopy. *Optics Express*, *24*(24), 27791. https://doi.org/10.1364/oe.24.027791

<img src="DH_tutorial_md.assets/image-20220506171904318.png" alt="image-20220506171904318" style="zoom:80%;" />



##### MWOPU examples: mkkim

- Kim, M. K. (2022). Phase microscopy and surface profilometry by digital holography. *Light: Advanced Manufacturing*, *3*(1), 1. https://doi.org/10.37188/lam.2022.019

![image-20220427214520872](DH_tutorial_md.assets/image-20220427214520872.png)

![image-20220427214628422](DH_tutorial_md.assets/image-20220427214628422.png)

![image-20220427214715153](DH_tutorial_md.assets/image-20220427214715153.png)

![image-20220427215024923](DH_tutorial_md.assets/image-20220427215024923.png)

![image-20220427215138931](DH_tutorial_md.assets/image-20220427215138931.png)





## Multi-Wavelength Generation

##### discrete lasers

##### tunable lsers

##### index tuning

##### angle scanning





## MAOPU

##### theory of MAOPU

##### MAOPU process

##### sample python code

##### MAOPU examples: mkkim

![image-20220427215312948](DH_tutorial_md.assets/image-20220427215312948.png)

![image-20220427215358192](DH_tutorial_md.assets/image-20220427215358192.png)

![image-20220427215431949](DH_tutorial_md.assets/image-20220427215431949.png)

![image-20220427215457707](DH_tutorial_md.assets/image-20220427215457707.png)

![image-20220427215537750](DH_tutorial_md.assets/image-20220427215537750.png)



##### MAOPU examples: survey





## WSOPU

##### WSQPM theory





##### WSOPU process

##### sample python code

##### WSOPU examples: mkkim

##### WSOPU examples: survey

- Li, Y., Xiao, W., & Pan, F. (2014). Multiple-wavelength-scanning-based phase unwrapping method for digital holographic microscopy. *APPLIED OPTICS*, *53*(5), 979–987. https://doi.org/10.1364/AO.53.000979
- Lédl, V., Psota, P., Kaván, F., Matoušek, O., & Mokrý, P. (2017). Surface topography measurement by frequency sweeping digital holography. *Applied Optics*, *56*(28), 7808. https://doi.org/10.1364/ao.56.007808

<img src="DH_tutorial_md.assets/image-20220429165841610.png" alt="image-20220429165841610" style="zoom:80%;" />

## ASOPU

##### theory of ASOPU

##### ASOPU process

##### sample python code

##### ASOPU examples: mkkim

##### ASOPU examples: survey

- Psota, P., Tang, H., Pooladvand, K., Furlong, C., Rosowski, J. J., Cheng, J. T., & Lédl, V. (2020). Multiple angle digital holography for the shape measurement of the unpainted tympanic membrane. *Optics Express*, *28*(17), 24614. https://doi.org/10.1364/oe.398919

<img src="DH_tutorial_md.assets/image-20220502140028547.png" alt="image-20220502140028547" style="zoom:80%;" />



## WSDIH

##### theory of WSDIH

##### WSDIH process

##### sample python code

##### WSDIH examples: mkkim

##### WSDIH examples: survey

- MARRON, J. C., & SCHROEDER, K. S. (1992). 3-DIMENSIONAL LENSLESS IMAGING USING LASER FREQUENCY DIVERSITY. *APPLIED OPTICS*, *31*(2), 255–262. https://doi.org/10.1364/AO.31.000255

![image-20220502215428846](DH_tutorial_md.assets/image-20220502215428846.png)

- MARRON, J. C., & SCHROEDER, K. S. (1993). HOLOGRAPHIC LASER-RADAR. *OPTICS LETTERS*, *18*(5), 385–387. https://doi.org/10.1364/OL.18.000385

![image-20220502221331902](DH_tutorial_md.assets/image-20220502221331902.png)

- ARONS, E., DILWORTH, D., SHIH, M., & SUN, P. C. (1993). USE OF FOURIER SYNTHESIS HOLOGRAPHY TO IMAGE THROUGH INHOMOGENEITIES. *OPTICS LETTERS*, *18*(21), 1852–1854. https://doi.org/10.1364/OL.18.001852
- Kim, M. K. (1999). Wavelength-scanning digital interference holography for optical section imaging. *OPTICS LETTERS*, *24*(23), 1693–1695. https://doi.org/10.1364/OL.24.001693

<img src="DH_tutorial_md.assets/image-20220502222058506.png" alt="image-20220502222058506" style="zoom:80%;" />

- Kim, M. K. (2000). Tomographic three-dimensional imaging of a biological specimen using wavelength-scanning digital interference holography. *OPTICS EXPRESS*, *7*(9), 305–310. https://doi.org/10.1364/OE.7.000305

<img src="DH_tutorial_md.assets/image-20220502222225664.png" alt="image-20220502222225664" style="zoom: 80%;" />

- Dakoff, A., Gass, J., & Kim, M. K. (2003). Microscopic three-dimensional imaging by digital interference holography. *JOURNAL OF ELECTRONIC IMAGING*, *12*(4), 643–647. https://doi.org/10.1117/1.1604784

<img src="DH_tutorial_md.assets/image-20220502222329616.png" alt="image-20220502222329616" style="zoom:67%;" />

- Yu, L. F., & Kim, M. K. (2005). Wavelength-scanning digital interference holography for tomographic three-dimensional imaging by use of the angular spectrum method. *OPTICS LETTERS*, *30*(16), 2092–2094. https://doi.org/10.1364/OL.30.002092

<img src="DH_tutorial_md.assets/image-20220502222504096.png" alt="image-20220502222504096" style="zoom:80%;" />

- Yu, L. F., & Kim, M. K. (2005). Wavelength scanning digital interference holography for variable tomographic scanning. *OPTICS EXPRESS*, *13*(15), 5621–5627. https://doi.org/10.1364/OPEX.13.005621
- Montfort, F., Colomb, T., Charriere, F., Kuehn, J., Marquet, P., Cuche, E., Herminjard, S., & Depeursinge, C. (2006). Submicrometer optical tomography by multiple-wavelength digital holographic microscopy. *APPLIED OPTICS*, *45*(32), 8209–8217. https://doi.org/10.1364/AO.45.008209
- Yu, L., & Chen, Z. (2007). Improved tomographic imaging of wavelength scanning digital holographic microscopy by use of digital spectral shaping. *OPTICS EXPRESS*, *15*(3), 878–886. https://doi.org/10.1364/OE.15.000878
- Kim, D., & Cho, Y. J. (2008). 3-D Surface Profile Measurement Using An Acousto-optic Tunable Filter Based Spectral Phase Shifting Technique. *JOURNAL OF THE OPTICAL SOCIETY OF KOREA*, *12*(4), 281–287. https://doi.org/10.3807/JOSK.2008.12.4.281
- Kuehn, J., Montfort, F., Colomb, T., Rappaz, B., Moratal, C., Pavillon, N., Marquet, P., & Depeursinge, C. (2009). Submicrometer tomography of cells by multiple-wavelength digital holographic microscopy in reflection. *OPTICS LETTERS*, *34*(5), 653–655.

<img src="DH_tutorial_md.assets/image-20220502223113698.png" alt="image-20220502223113698" style="zoom:80%;" />

- Potcoava, M. C., & Kim, M. K. (2009). Fingerprint biometry applications of digital holography and low-coherence interferography. *APPLIED OPTICS*, *48*(34), H9–H15. https://doi.org/10.1364/AO.48.0000H9

<img src="DH_tutorial_md.assets/image-20220502223320459.png" alt="image-20220502223320459" style="zoom:80%;" />

- Potcoava, M. C., Kay, C. N., Kim, M. K., & Richards, D. W. (2010). In vitro imaging of ophthalmic tissue by digital interference holography. *JOURNAL OF MODERN OPTICS*, *57*(2, SI), 115–123. https://doi.org/10.1080/09500340903045686

<img src="DH_tutorial_md.assets/image-20220502223428429.png" alt="image-20220502223428429" style="zoom:67%;" />

- Xu, L., Mater, M., & Ni, J. (2011). Focus detection criterion for refocusing in multi-wavelength digital holography. *OPTICS EXPRESS*, *19*(16), 14779–14793. https://doi.org/10.1364/OE.19.014779

<img src="DH_tutorial_md.assets/image-20220506154214147.png" alt="image-20220506154214147" style="zoom:50%;" />

- Xu, L., Aleksoff, C. C., & Ni, J. (2012). High-precision three-dimensional shape reconstruction via digital refocusing in multi-wavelength digital holography. *APPLIED OPTICS*, *51*(15), 2958–2967. https://doi.org/10.1364/AO.51.002958

<img src="DH_tutorial_md.assets/image-20220506161850832.png" alt="image-20220506161850832" style="zoom:67%;" />

- Chen, S., Ryu, J., Lee, K., & Zhu, Y. (2016). Swept source digital holographic phase microscopy. *OPTICS LETTERS*, *41*(4), 665–668. https://doi.org/10.1364/OL.41.000665

<img src="DH_tutorial_md.assets/image-20220506162020326.png" alt="image-20220506162020326" style="zoom:67%;" />





## ASDIH

##### theory of ASDIH

##### ASDIH process

##### sample python code

##### ASDIH examples: mkkim

##### ASDIH examples: survey

- Jeong, S. J., & Hong, C. K. (2008). Illumination-angle-scanning digital interference holography for optical section imaging. *OPTICS LETTERS*, *33*(20), 2392–2394. https://doi.org/10.1364/OL.33.002392
- Jeon, Y., & Hong, C. K. (2010). Optical section imaging of the tilted planes by illumination-angle-scanning digital interference holography. *APPLIED OPTICS*, *49*(27), 5110–5116. https://doi.org/10.1364/AO.49.005110

<img src="DH_tutorial_md.assets/image-20220429162140423.png" alt="image-20220429162140423" style="zoom:80%;" />

- Dong, J., Jia, S., & Jiang, C. (2017). Surface shape measurement by multi-illumination lensless Fourier transform digital holographic interferometry. *Optics Communications*, *402*(May), 91–96. https://doi.org/10.1016/j.optcom.2017.05.051

<img src="DH_tutorial_md.assets/image-20220429161726446.png" alt="image-20220429161726446" style="zoom:80%;" />

- Martinez-Carranza, J., Mikuła-Zdańkowska, M., Ziemczonok, M., & Kozacki, T. (2020). Multi-incidence digital holographic profilometry with high axial resolution and enlarged measurement range. *Optics Express*, *28*(6), 8185. https://doi.org/10.1364/oe.385743

<img src="DH_tutorial_md.assets/image-20220429160809187.png" alt="image-20220429160809187" style="zoom:80%;" />



|        | wavelength | angle |      |      |
| ------ | ---------- | ----- | ---- | ---- |
| 1W QPM | QPM        |       |      |      |
| 2W QPM | 2WOPU      | 2AOPU |      |      |
| MW QPM | MWOPU      | MAOPU |      |      |
| WS QPM | WSOPU      | ASOPU |      |      |
| WS DIH | WSDIH      | ASDIH |      |      |
|        |            |       |      |      |





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

- Jeon, Y. & Hong, C. K. Optical section imaging of the tilted planes byillumination-angle-scanning  digital  interference  holography. AppliedOptics49, 5110-5116 (2010).
- Dong, J., J ia, S. H. & Jiang, C. Surface shape measurement by multi-illumination   lensless   Fourier   transform   digital   holographicinterferometry. Optics Communications402, 91-96 (2017).







------

##### DHM examples: survey



##### multi-wavelength: history



##### wavelength-scanning: history



##### 2WOPU examples: survey



##### MWOPU examples: survey



##### WSDIH examples: survey



##### MAOPU examples: survey



##### ASDIH examples: survey







## todolist: 6/2/2022

- [x] h-mwopu theory
- [x] h-mwopu sim
- [x] h-mwopu example
- [x] c-mwopu theory 
- [ ] c-mwopu sim
- [x] c-mwopu example
- [x] wsdih theory
- [ ] wsdih sim
- [x] wsdih example
- [ ] wlen vs ang theory
- [x] h-maopu example
- [x] c-maopu example
- [x] asdih example
- [ ] compare h-opu vs c-opu vs dih theory & sim
- [ ] compare h-maopu vs c-maopu vs asdih expt





### c-mwopu theory & sim

$$
\Phi_n = \left[2\pi\frac{Z}{\lambda_n}\right]//2\pi \\
\Phi_{12} = \Phi_1 - \Phi_2 = 2\pi Z \left[\frac{1}{\lambda_1}-\frac{1}{\lambda_2}\right] = 2\pi\frac{Z}{\Lambda_{12}} \qquad [\Lambda_{12}>Z_{\max}] \\
Z_{12} = \Lambda_{12}\frac{\Phi_{12}}{2\pi}
$$

- choose $\displaystyle\frac{1}{\lambda_n}$  at uniform intervals: 

$$
\frac{1}{\lambda_1}-\frac{1}{\lambda_2}=\frac{1}{\lambda_2}-\frac{1}{\lambda_3}=\cdots\equiv\frac{1}{\Lambda}
$$

$$
\Phi_{12}=\Phi_1 - \Phi_2 = 2\pi Z \left[ \frac{1}{\lambda_1} - \frac{1}{\lambda_2} \right] = 2\pi \frac{Z}{\Lambda} \\
\Phi_{23}=\Phi_2 - \Phi_3 = 2\pi Z \left[ \frac{1}{\lambda_2} - \frac{1}{\lambda_3} \right] = 2\pi \frac{Z}{\Lambda} \\
\cdots \\
\Phi_{n,n+1}=\Phi_n - \Phi_{n+1} = 2\pi Z \left[ \frac{1}{\lambda_n} - \frac{1}{\lambda_{n+1}} \right] = 2\pi \frac{Z}{\Lambda} \\
\\
\tilde\Phi_{1n}=\Phi_{12} + \Phi_{23} + \cdots +\Phi_{n,n+1} = \Phi_1 - \Phi_{n+1} = 2\pi Z\left[\frac{1}{\lambda_1} - \frac{1}{\lambda_{n+1}} \right] = 2\pi n\frac{Z}{\Lambda} \\
\\
\tilde Z_{1n} = \frac{\Lambda}{n}\frac{\tilde\Phi_{1n}}{2\pi}
$$

- noise in $\tilde Z_{1n}$:

$$
\delta\tilde Z_{1n} = \frac{\Lambda}{2\pi n}\sqrt{2}\ 2\pi\epsilon = \frac{\sqrt{2}\epsilon\Lambda}{n} = \frac{\delta Z_{12}}{n} = \delta Z_{1,n+1}
$$



### wsdih theory





























