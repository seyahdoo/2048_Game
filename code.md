# 2048_Game
pascal codes of my 2048 game


program thousandv3;
uses crt;
var       actual,undo1,undo2,undo3,undo4,undo5:array [1..20,1..20] of integer;
          random2i,random2j:array[1..400] of integer;
          puan,eskipuan1,eskipuan2,eskipuan3,eskipuan4,eskipuan5:integer;
          i,j,newi,newj,k,oyun_buyuklugu,randomtwoorfour:byte;
          key:char;
          ismoved,isfinished,isasked:boolean;
procedure matrix_yazdir;
begin


         if oyun_buyuklugu=4 then begin


         clrscr;
         write(chr(201),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(187));writeln();
         write(chr(204),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),'2048',chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(205),chr(185));writeln();
         write(chr(204),chr(205),chr(205),chr(205),chr(205),chr(203),chr(205),chr(205),chr(205),chr(205),chr(203),chr(205),chr(205),chr(205),chr(205),chr(203),chr(205),chr(205),chr(205),chr(205),chr(185));writeln();

         for i:=1 to 4 do begin
            write(chr(186));
            for j:=1 to 4 do begin

                 case (actual[i,j]) of
           0 :    TextColor(7);  //white
           2 :    TextColor(4);  //red
           4 :    TextColor(1);  //blue
           8 :    TextColor(2);  //green
           16 :   TextColor(3);  //cyan
           32 :   TextColor(6);  //brown
           64 :   TextColor(12); //Light red
           128 :  TextColor(9);  //light blue
           256 :  TextColor(10); //light Green
           512 :  TextColor(11); //Light Cyan
           1024 : TextColor(14); //Yellow
           2048 : TextColor(5);  //Magenta
           end;

                if ((i=newi) and (j=newj)) then   begin
                write(actual[i,j]:3); TextColor(7);write('*'); write(chr(186));
                end else begin
                write(actual[i,j]:4); TextColor(7); write(chr(186));
                end;
            end;
            writeln();
         end;
         write(chr(200),chr(205),chr(205),chr(205),chr(205),chr(202),chr(205),chr(205),chr(205),chr(205),chr(202),chr(205),chr(205),chr(205),chr(205),chr(202),chr(205),chr(205),chr(205),chr(205),chr(188));writeln();

         writeln();
         write('PUAN:'); write(puan);

         end else begin

         clrscr;
         for i:=1 to oyun_buyuklugu do begin
           for j:=1 to oyun_buyuklugu do begin
           case (actual[i,j]) of
           0 :    TextColor(7);  //white
           2 :    TextColor(4);  //red
           4 :    TextColor(1);  //blue
           8 :    TextColor(2);  //green
           16 :   TextColor(3);  //cyan
           32 :   TextColor(6);  //brown
           64 :   TextColor(12); //Light red
           128 :  TextColor(9);  //light blue
           256 :  TextColor(10); //light Green
           512 :  TextColor(11); //Light Cyan
           1024 : TextColor(14); //Yellow
           2048 : TextColor(5);  //Magenta
           end;

           write(actual[i,j]:4);write('  ');
           end;
           writeln();writeln();writeln();
         end;
         writeln();
         writeln();
         TextColor(7);
         write('PUAN: ');write(puan);

         end;


   {matrix kontrol}


         for i:=1 to oyun_buyuklugu do begin
             for j:=1 to oyun_buyuklugu do begin


             end;
         end;

end;
procedure iki_koy;
begin
         if ismoved=true then begin
          {2 or 4}
         if random(10)=0 then begin
          randomtwoorfour:=4;
         end
          else begin
          randomtwoorfour:=2;
         end;
           {2 or 4}

          k:=0;
          for i:=1 to oyun_buyuklugu do begin
             for j:=1 to oyun_buyuklugu do begin
               if actual[i,j]=0 then  begin
               k:=k+1;
               random2i[k]:=i;
               random2j[k]:=j;
               end;
             end;
          end;

          k:=random(k)+1;
          actual[random2i[k],random2j[k]]:=randomtwoorfour;
          newi:=random2i[k];
          newj:=random2j[k];


     ismoved:=false;

         if isasked=false then begin
         for i:=1 to oyun_buyuklugu do begin         //kazandığını kontrol et
             for j:=1 to oyun_buyuklugu do begin

                 if actual[i,j]=2048 then begin
                    matrix_yazdir;
                    writeln('KAZANDINIZ');writeln();
                    writeln('devam etmek istiyor musunuz? (e veya h, ye basin.)');
                    isasked:=true;
                    key:=readkey;
                    if key='h' then begin
                    halt(1);  end;
                 end;
             end;
         end;
       end;



         end  else begin

         isfinished:=true;
         for i:=1 to oyun_buyuklugu do begin              //bittiğini kontrol et
             for j:=1 to oyun_buyuklugu do begin

                 if actual[i,j]=0 then begin
                 isfinished:=false

                 end;

                 if (actual[i,j]=2048) and (isasked=false) then begin
                    writeln('KAZANDINIZ');writeln();
                    writeln('devam etmek istiyor musunuz? (e veya h, ye basin.)');
                    key:=readkey;
                    if key='h' then begin
                    halt(1);  end;
                 end;
             end;
         end;
         if isfinished=true then begin
         writeln();writeln('kusura bakma haci ama, bu oyun burda biter...');
         readkey;
         halt(2);

         end;
         end;
end;
procedure saga_cek;
begin
     for i:=1 to oyun_buyuklugu do begin
       k:=oyun_buyuklugu-1;
       while (k<>0) do begin
       if (actual[i,k] <> 0) then begin
        while (((actual[i,k]<>0) and (actual[i,k+1]=0)) and (k<>oyun_buyuklugu)) do begin
           actual[i,k+1]:=actual[i,k];
           actual[i,k]:=0;
           k:=k+1;
           ismoved:=True;
        end;
        k:=k-1;
     end else  begin
          k:=k-1;
        end;
     end;  end;
end;
procedure sola_cek;
begin
     for i:=1 to oyun_buyuklugu do begin
       k:=1;
       while (k<>oyun_buyuklugu+1) do begin
       if (actual[i,k] <> 0) then begin
        while (((actual[i,k]<>0) and (actual[i,k-1]=0)) and (k<>1)) do begin
           actual[i,k-1]:=actual[i,k];
           actual[i,k]:=0;
           k:=k-1;
           ismoved:=True;
        end;
        k:=k+1;
     end else  begin
          k:=k+1;
        end;
     end;  end;
end;
procedure assagi_cek;
begin
     for i:=1 to oyun_buyuklugu do begin
       k:=oyun_buyuklugu-1;
       while (k<>0) do begin
       if (actual[k,i] <> 0) then begin
        while (((actual[k,i]<>0) and (actual[k+1,i]=0)) and (k<>oyun_buyuklugu)) do begin
           actual[k+1,i]:=actual[k,i];
           actual[k,i]:=0;
           k:=k+1;
           ismoved:=True;
        end;
        k:=k-1;
     end else  begin
          k:=k-1;
        end;
     end;  end;
end;
procedure yukari_cek;
begin
     for i:=1 to oyun_buyuklugu do begin
       k:=1;
       while (k<>oyun_buyuklugu+1) do begin
       if (actual[k,i] <> 0) then begin
        while (((actual[k,i]<>0) and (actual[k-1,i]=0)) and (k<>1)) do begin
           actual[k-1,i]:=actual[k,i];
           actual[k,i]:=0;
           k:=k-1;
           ismoved:=True;
        end;
        k:=k+1;
     end else  begin
          k:=k+1;
        end;
     end;  end;
end;
procedure saga_topla;
begin
     for i:=1 to oyun_buyuklugu do begin
      for k:=oyun_buyuklugu-1 downto 1 do begin
      if ((actual[i,k]=actual[i,k+1]) and (actual[i,k]<>0)) then begin
       actual[i,k+1]:=actual[i,k+1]+actual[i,k+1];
       actual[i,k]:=0;
       puan:=puan+actual[i,k+1];
       ismoved:=True;
      end;     end;   end;    end;
procedure sola_topla;
begin
     for i:=1 to oyun_buyuklugu do begin
      for k:=2 to oyun_buyuklugu do begin
      if ((actual[i,k]=actual[i,k-1]) and (actual[i,k]<>0)) then begin
       actual[i,k-1]:=actual[i,k-1]+actual[i,k-1];
       actual[i,k]:=0;
       puan:=puan+actual[i,k-1];
       ismoved:=True;
      end;     end;   end;  end;
procedure assagi_topla;
begin
     for i:=1 to oyun_buyuklugu do begin
      for k:=oyun_buyuklugu-1 downto 1 do begin
      if ((actual[k,i]=actual[k+1,i]) and (actual[k,i]<>0)) then begin
       actual[k+1,i]:=actual[k+1,i]+actual[k+1,i];
       actual[k,i]:=0;
       puan:=puan+actual[k+1,i];
       ismoved:=True;
      end;     end;   end;  end;
procedure yukari_topla;
begin
     for i:=1 to oyun_buyuklugu do begin
      for k:=2 to oyun_buyuklugu do begin
      if ((actual[k,i]=actual[k-1,i]) and (actual[k,i]<>0)) then begin
       actual[k-1,i]:=actual[k-1,i]+actual[k-1,i];
       actual[k,i]:=0;
       puan:=puan+actual[k-1,i];
       ismoved:=True;
      end;     end;   end;  end;
procedure undo;
begin
      actual:=undo1;
      undo1:=undo2;
      undo2:=undo3;
      undo3:=undo4;
      undo4:=undo5;

      puan:=eskipuan1;
      eskipuan1:=eskipuan2;
      eskipuan2:=eskipuan3;
      eskipuan3:=eskipuan4;
      eskipuan4:=eskipuan5;
end;
procedure matrix_kaydet;
begin
     undo5:=undo4;
     undo4:=undo3;
     undo3:=undo2;
     undo2:=undo1;
     undo1:=actual;

     eskipuan5:=eskipuan4;
     eskipuan4:=eskipuan3;
     eskipuan3:=eskipuan2;
     eskipuan2:=eskipuan1;
     eskipuan1:=puan;
end;

begin
       randomize();
       write('kare oyun buyuklugunu girin(2-7): ');read(oyun_buyuklugu);
       ismoved:=True;
       isasked:=false;
       puan:=0;
       iki_koy;
       ismoved:=true;
       iki_koy;
       while true do begin
       matrix_yazdir;
       key:=readkey;

       case key of
       'a' : begin
       matrix_kaydet;
       sola_cek;
       sola_topla;
       sola_cek;
       iki_koy;
       end;

       's' : begin
       matrix_kaydet;
       assagi_cek;
       assagi_topla;
       assagi_cek;
       iki_koy;
       end;

       'd' : begin
       matrix_kaydet;
       saga_cek;
       saga_topla;
       saga_cek;
       iki_koy;
       end;

       'w' : begin
       matrix_kaydet;
       yukari_cek;
       yukari_topla;
       yukari_cek;
       iki_koy;
       end;

       'p' : begin
       actual[1,1]:=1024;   //test için.
       actual[1,2]:=1024;
       actual[1,3]:=2;
       actual[1,4]:=2;
       actual[2,1]:=2;
       actual[2,2]:=2;
       actual[2,3]:=2;
       actual[2,4]:=2;
       actual[3,1]:=2;
       actual[3,2]:=2;
       actual[3,3]:=2;
       actual[3,4]:=0;
       actual[4,1]:=0;
       actual[4,2]:=0;
       actual[4,3]:=0;
       actual[4,4]:=0;
       end;

       'r' : begin

       undo;
       end;

       'e' : begin
       writeln();
       writeln('oyunu bitirdiniz.');
       readkey;
       halt(3);
       end;
    end;



       end;
end.
