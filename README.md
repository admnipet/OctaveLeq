# OctaveLeq
Algortihm to calculate the Leq in Octave

This code is meant for calculating the LEQ in matlab. Below you can find the whole source code.

%Lärmäquivalenzmessungsalgorithmus
%Version 0.8 
%Last Change *Current Date*
%Author: Nikola Petkovic

  clear;
  clc;
  
%datei einlesen und auf fehler prüfuen

  fid = fopen('2021-5-3 15-56.txt','r');
 
%wenn dateiname falsch, Fehler ausgeben
if fid == -1     
  disp('Fehler, untersuchen sie den Dateinamen oder den Speicherort');
  else  
%Datei laden und ohne header scannen 
  m = textscan(fid, '%s %s %f %s', 'Headerlines' , 2);
  
%tag aus der txt ziehen
  tag = cell2mat(m{1});

%skalen in strings umwandeln
  for i = 1:length(m{2});
      
      m{2}{i}=m{2}{i}(4:8);
      m{2}{i}(3)=".";
      m{2}{i}=str2num(m{2}{i});
      
      endfor  
%Werte zuweisen / Zellen in Matrix umwandeln 
  zeit = cell2mat(m{2});
  wert = m{3};
  einheit = cell2mat(m{4});
  
%f1 = Leq mit fortlaufendem wert
  f1 = figure(1);
  
  x1 = zeit;
  ti= (0.5);
  q = (3);
  L1 = q/(log10(2));%9.9658 
  L2 = log10(2/q); %-0.17609
  Leq = L1*log10(1/(x1.*wert.*ti*10*L2));
  
 % Leq= q/(log10(2))*Log10(1/(zeit1*) //8 Stunden lange Messung// 6 Stunden
  
  plot(Leq); 
  xlabel('Zeit in s'), ylabel('Wert in dBA'),title('Energie-äquivalenter Dauerschallpegel (Leq)'),set(gca,'fontsize',15); grid on   

%f2 = standard wert der Funktion  
  f2 = figure(2)  
  y2 = wert;
  x2 = zeit;
%Plot der normalen Funktion zum besseren analysiere der Normalverteilugn des Programmes  
  plot(x2,y2);
  xlabel('Zeit in s'), ylabel('Wert in dBA'),title('Alle Messwerte'),set(gca,'fontsize',20); grid on  

%f4 = alle Peaks der Leq
  f3=figure(3);
  peaks(zeit,wert,zeit);
  xlabel('Zeit in s'), ylabel('Lautstärke in DB'),title('Peaks der Messwerte'),set(gca,'fontsize',15); grid on  
 
 %new shit on the way for some of that shit. 
 %chasing new money machine on there (upgrade next variable to be better)
 
 end
  fclose(fid);
