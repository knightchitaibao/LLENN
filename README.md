# LLENN
A neural network of OFC dynamics

## Data Description
The data is from the evolution of a soliton comb in a silica microshpere. 
The parameters of the system is given in **PILLE.ipynb**.

## LLE Equation
1. 

$$\frac{\partial A}{\partial t}=-{\alpha} A - \text{i}\Delta A + \text{i}\frac{D_2}{2} \frac{\partial^2 A}{\partial \phi^2}+ \text{i} g|A|^2A + \sqrt{\frac{\alpha}{2}}A_{\text{in}}$$   
$$
    \frac{\partial A}{\partial t}=-{\alpha} A - \text{i}\Delta A - \text{i}\sum_{k\geq 2} \frac{i^kD_k}{k!} \frac{\partial^k A}{\partial \phi^k}+ \text{i} g|A|^2A + \sqrt{\frac{\alpha}{2}}A_{\text{in}} 
$$
    
$$
    \frac{\partial A_m}{\partial t}=-{\alpha} A_m - \text{i}\Delta A_m -\text{i}\sum_{k\geq 2} \frac{i^{2k}D_km^k}{k!} A_m+ \text{i} g\text{FFT}[|A|^2A]_m + \sqrt{\frac{\alpha}{2}}A_{\text{in}_{m}} 
$$
    
$$
    \frac{\partial A_m}{\partial t}=-({\alpha}  + \text{i}\Delta) A_m -\text{i}\sum_{k\geq 2} \frac{(-1)^{k}D_km^k}{k!} A_m+ \text{i} g\text{FFT}[|A|^2A]_m + \sqrt{\frac{\alpha}{2}}A_{\text{in}_{m}} 
$$
    
1. The loss term $\alpha =\frac{\kappa}{2} = \frac{1}{2\tau}=\frac{\pi\nu}{Q}$
    $\tau$ is the photon lifetime. $Q$ is the quality factor of cavity.
2. The detuning term $\Delta = \omega_{\text{resonance}}-\omega_{\text{pump}}$
    $\omega_{\text{resonance}}$ and $\omega_{\text{pump}}$ will be represent by $\omega_0$ and $\omega_\text{p}$
3. The dispersion term $D_2$
4. The nonlinear term $g = \frac{\hbar\omega_0^2 n_2 D_1}{2\pi n_0 A_{\text{eff}}}$
5. The pump term $\sqrt{\frac{\alpha}{2}}A_{\text{in}}$ 
    By default, we assume the system is in the critical coupling. Generally, this term is $\sqrt{\kappa}=\sqrt{\alpha\eta}$. $\kappa$ is the coupling loss.
1. Fundamental Phase Domain **NLSE** in $(t,\phi)$ Space
$t$ is the slow time which imply the position of field. It only obtains the actual physical meaning when $t=m\tau_R$. $\tau_R$ is the roundtrip time in which the field finish a cycle in cavity. $\phi$ is the phase of the field. 
Significantly, $A$ is a function about photon number, which means $|A|^2$ is the photon number of the field.

$\frac{\partial A}{\partial t}=-{\alpha} A - \text{i}\Delta A + \text{i}\frac{D_2}{2} \frac{\partial^2 A}{\partial \phi^2}+ \text{i} g|A|^2A + \sqrt{\frac{\alpha}{2}}A_{\text{in}}$    

1. The loss term $\alpha =\frac{\kappa}{2} = \frac{1}{2\tau}=\frac{\pi\nu}{Q}$
    $\tau$ is the photon lifetime. $Q$ is the quality factor of cavity.
2. The detuning term $\Delta = \omega_{\text{resonance}}-\omega_{\text{pump}}$
    $\omega_{\text{resonance}}$ and $\omega_{\text{pump}}$ will be represent by $\omega_0$ and $\omega_\text{p}$
3. The dispersion term $D_2$
4. The nonlinear term $g = \frac{\hbar\omega_0^2 n_2 D_1}{2\pi n_0 A_{\text{eff}}}$
5. The pump term $\sqrt{\frac{\alpha}{2}}A_{\text{in}}$ 
    By default, we assume the system is in the critical coupling. Generally, this term is $\sqrt{\kappa}=\sqrt{\alpha\eta}$. $\kappa$ is the coupling loss.
1. Phase Domain **GNLSE** in $(t,\phi)$ Space
By the transformation in the bottom, we can derivate the GNLSE: 

$\frac{\partial A}{\partial t}=-A - \text{i}\Delta A - \text{i}sgn(-D_2) \frac{\partial^2 A}{\partial \phi^2}+ \text{i} |A|^2A + S_{in}$ 
The common expression multiplies $i$ in the equation: 

$i\frac{\partial A}{\partial t} - sgn(-D_2) \frac{\partial^2 A}{\partial \phi^2} +|A|^2A- \Delta A=-\text{i}A  + \text{i}S_{in}$ 
What we concerned is the anomalous dispersion region, so $sgn(-D_2)=-1$ and the equation can be written: 

$\frac{\partial A}{\partial t}=-A - \text{i}\Delta A + \text{i} \frac{\partial^2 A}{\partial \phi^2}+ \text{i} |A|^2A + S_{in}$ 
$i\frac{\partial A}{\partial t}+ \frac{\partial^2 A}{\partial \phi^2} +|A|^2A- \Delta A=-\text{i}A  + \text{i}S_{in}$ 

    
$$
    \text{varible transformation: }\begin{cases}
    A\to\sqrt{{\frac{g}{\alpha}}}{A}\\ 
    \phi\to\sqrt{\frac{2\alpha}{|D_2|}}{\phi}\\
    t\to \alpha t
    \end{cases}
$$
    
$$
    \text{coefficient description:}\begin{cases}
    \Delta=\frac{\omega_0-\omega_{\text{p}}}{\alpha}\\ 
    S_{\text{in}}=\sqrt{\frac{g}{2\alpha^2}}A_{\text{in}}
    \end{cases}
$$
    
<aside>
    💡 Other popular expression and corresponding transition
    
1. $i\frac{\partial A}{\partial t}+ \frac{\partial^2 A}{\partial \phi^2} +2|A|^2A- \Delta A=-\text{i}A  + \text{i}S_{in}$ 
The generalized equation can be obtained from the above by:
        
$$
        \text{varible transformation: }\begin{cases}
        A\to\sqrt{{\frac{1}{2}}}{A}
        \end{cases}    $$
        
2. $i\frac{\partial A}{\partial t}+ \frac{1}{2}\frac{\partial^2 A}{\partial \phi^2} +|A|^2A- \Delta A=-\text{i}A  + \text{i}S_{in}$ 
    The generalized equation can be obtained from the above by:
        
$$
        \text{varible transformation: }\begin{cases} 
        \phi\to\sqrt{\frac{1}{2}}{\phi}
        \end{cases}
        $$
        
</aside>
    
4. Pseudo-frequency Domain NLSEs in $(t,\nu\tau_R)$ Space from  $(t,\phi)$ Space
It’s worth nothing that $A$ is the envelope of field, so its frequency is the difference from the resonance frequency. So $A=A(t)e^{-i\delta\nu\tau_R\phi},\delta\nu=\nu - \nu_p$ . Then we can write the frequency domain NLSEs:
 
$\frac{\partial A_\nu}{\partial t}=-\alpha A_\nu - \text{i}\Delta A_\nu + \text{i}\frac{D_2}{2} (\delta\nu\tau_R)^2 A_\nu+ \text{i} g[|A|^2A]_\nu + \sqrt{\frac{\alpha}{2}}A_{\text{in}}$ 

The subscript $\nu$ means the time-dependent transform into $\nu$-dependent. $A_\nu=F_\nu(A)$ .

5. Pseudo-frequency Domain GNLSEs in $(t,\nu\tau_R)$ Space from  $(t,\phi)$ Space
Following the above, GNLSEs in frequency domain can be written: 
          
$\frac{\partial A_\nu}{\partial t}=-A_\nu - \text{i}\Delta A_\nu - \text{i}sgn(-D_2)(\delta\nu\tau_R)^2 A_\nu+ \text{i} |A|^2A_\nu + S_{\text{in}}$ 

But what need to be noticed is the transformation $\phi\to\sqrt{\frac{2\alpha}{|D_2|}}{\phi}$  has been done. So the actual frequency difference $\delta\nu_{\text{actual}} = \sqrt{\frac{2\alpha}{|D_2|}}\delta\nu_{\text{normilized}}$. 

6. Azimuthal Mode Number Domain NLSEs in $(t,m)$ Space from  $(t,\phi)$ Space
If we only take account of the linear frequency shift, there is $\delta\nu=m\Delta\nu_{\text{FSR}}$ which means $\delta\nu\tau_R=m(\Delta\nu_{\text{FSR}}\tau_R)=m$. Coincidentally and Explicitly,  Pseudo-frequency Domain NLSEs is azimuthal mode number domain NLSEs in reality. 

$\frac{\partial A_m}{\partial t}=-\alpha A_m - \text{i}\Delta A_m - \text{i}\frac{D_2}{2}m^2 A_m+ \text{i}g |A|^2A_m + \sqrt{\frac{\alpha}{2}}A_{\text{in}}$ 

The subscript $m$ means the time-dependent transform into $m$-dependent. But $A_m=A_{m\Delta\nu_{\text{FSR}}}$

7. Azimuthal Mode Number Domain GNLSEs in $(t,m)$ Space from  $(t,\phi)$ Space
Similarly, Azimuthal Mode Number Domain GNLSEs can be written: 
                     
$\frac{\partial A_m}{\partial t}=-A_m - \text{i}\Delta A_m - \text{i}sgn(-D_2)m^2 A_m+ \text{i} [|A|^2A]_m + S_{\text{in}}$ 

8. Appendix 
    1. Phase domain NLSE in $(t,\tau)$ space
    
$\frac{\partial A}{\partial t}=-\alpha A - \text{i}\Delta A - \text{i}\frac{\beta_2}{2} \frac{\partial^2 A}{\partial \tau^2}+ \text{i} g|A|^2A + \sqrt{\frac{\alpha}{2}}A_{\text{in}}$ 
    
2. Phase domain GNLSE in $(t,\tau)$ space
    TODO
$\frac{\partial A}{\partial t}=-\alpha A - \text{i}\Delta A - \text{i}\frac{\beta_2}{2} \frac{\partial^2 A}{\partial \tau^2}+ \text{i} g|A|^2A + \sqrt{\frac{\alpha}{2}}A_{\text{in}}$