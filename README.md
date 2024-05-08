method%1.pitch estimation using manual method
 
[x,fs]=audioread('C:\Program Files\MATLAB\MATLAB Production Server\R2015a\bin\work\data\1-11.wav');
plot(x);axis tight;grid on;
 
sample=ginput(5);
pp=diff(sample)/fs;
% diff(X), for a vector X, is [X(2)-X(1)  X(3)-X(2) ... X(n)-X(n-1)].
pf=1./pp;
 
%2.a)pitch period estimation using autocorrelation
[x,fs]=audioread('C:\Program Files\MATLAB\MATLAB Production Server\R2015a\bin\work\data\1-11.wav');
b=fir1(51,0.05);
x_filter=filter(b,1,x);
subplot(211),plot(x);axis tight;grid on;
subplot(212),plot(x_filter);axis tight;grid on;
y1=x_filter(5000:5400);
plot(y1);axis tight;grid on;
x_corr=xcorr(y1);
plot(x_corr);axis tight;grid on;
instants=ginput(2);
pp=instants/fs;
pf=1./pp;




Pitch frequency = 117Hz, 77 Hz
%2.b)pitch estimation using autocorrelation
[x,fs]=audioread('C:\Program Files\MATLAB\MATLAB Production Server\R2015a\bin\work\data\1-11.wav');
plot(x);axis tight;grid on;
[f0,loc] =pitch(x,fs);
plot(f0);

% f0 = pitch(...,'Range',RANGE) limits the search range for the pitch
%     between the specified lower and upper band edges, inclusive. Specify
%     range in Hz as a two-element row vector of increasing values. If
%     unspecified, RANGE defaults to [50,400].
% f0 = pitch(...,'WindowLength',WINDOWLENGTH) specifies the analysis
%     window length used to calculate pitch. Specify the window length in
%     samples as a positive scalar. The maximum window length is 192000. If
%     unspecified, WINDOWLENGTH defaults to round(fs*0.052).
% f0 = pitch(...,'OverlapLength',OVERLAPLENGTH) specifies the number of
%     samples overlap between adjacent windows. Specify the overlap length as
%     a positive scalar smaller than the window length. If unspecified,
%     OVERLAPLENGTH defaults to round(fs*(0.042)).
% f0 = pitch(...,'Method',METHOD) specifies the method used to calculate
%     the pitch. Valid inputs are:
%          PEF - Pitch Estimation Filter
%          NCF - Normalized Correlation Function
%          CEP - Cepstrum
%          LHS - Log-harmonic Summation
%          SRH - Summation of Residual Harmonics
%     If unspecified, METHOD defaults to 'NCF'.
