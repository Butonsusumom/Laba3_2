# Calculation of a definite integral
## Analysis of two different ways of subtraction of a certain intgeral. (Condition in the report)

>Delphi

```dpr
program LR3_2;

{$APPTYPE CONSOLE}

uses

SysUtils;

type

TInt = function(x: real): Real;

procedure Method1(Int: TInt; a, b: real);

var S, h, Prev, e: real;

n,i, ie: integer;

begin

S:=Int(a)*(b-a);

e:=0.01;

n:=1;

if abs(S)<e then

begin

write(S:9:4,'|',n:3,'|');

end

else

begin

n:=5;

ie:=2;

while ie<=3 do

begin

repeat

Prev:=S;

S:=0;

h:=(b-a)/n;

for i:=1 to n do

S:=S+h*Int(a+i*h);

n:=n+5;

until abs(S-Prev)<e;

Write(S:9:6,'|',n-5:3,'|');

e:=0.001;

inc(ie);

end;

end;

end;

function Int3(x:real):Real;

begin

result:=1/(Sqrt(Sqr(x)+3.2));

end;

function Int4(x:Real):Real;

begin

Result:=(x+1)*Sin(x);

end;

procedure Method2(a,b:Real;Int:TInt);

var h,Iprev,Icur,E:Real;

n,i,ie:integer;

begin

Icur:=Int(a+h/2)*(b-a);

E:=0.01;

n:=1;

if abs(Icur)<E then

begin

write(Icur:9:4,'|',n:3,'|');

end

else

begin

n:=5;

ie:=2;

while ie<=3 do

begin

repeat

Iprev:=Icur;

Icur:=0;

h:=(b-a)/n;

for i:=0 to n-1 do

begin

Icur:=Icur+Int(a+h/2+i*h);

end;

Icur:=h*Icur;

n:=n+5;

until Abs(Icur-Iprev)< E;

Write(Icur:9:6,'|',n-5:3,'|');

inc(ie);

E:=0.001;

end;

end;

end;

procedure head;

begin

Writeln('|------------------------------------------------------------------|');

writeln('| | 1 method | 2 method |');

Writeln('| |---------------------------|---------------------------|');

writeln('| | e=10^-2 | e=10^-3 | e=10^-2 | e=10^-3 |');

Writeln('| |-------------|-------------|-------------|-------------|');

writeln('| | value | N | value | N | value | N | value | N |');

Writeln('|----------|-------------|-------------|-------------|-------------|');

end;

procedure row(n:integer);

begin

write('|',n,' integral|');

end;

function Int1(x:real):Real;

begin

result:=Sqrt(0.5*x+2)/(Sqrt(2*x*x+1)+0.8);

end;

function Int2(x:real):Real;

begin

result:=Cos(0.8*x+1.2)/(1.5+sin(x*x+0.6));

end;

var k:Integer;

Int:TInt;

begin

head;

k:=1;

while k<=4 do

begin

case k of

1: begin

row(k);

Int:=Int1;

Method1(Int,0.4,1.2);

Method2(0.4,1.2,Int);

Writeln;

Writeln('|----------|-------------|-------------|-------------|-------------|');

end;

2: begin

row(k);

Int:=Int2;

Method1(Int,0.3,0.9);

Method2(0.3,0.9,Int);

writeln;

Writeln('|----------|-------------|-------------|-------------|-------------|');

end;

3: begin

row(k);

Method1(Int,1.2,2.7);

Method2(1.2,2.7,Int);

writeln;

Writeln('|----------|-------------|-------------|-------------|-------------|');

end;

4: begin

row(k);

Int:=Int4;

Method1(Int,1.6,2.4);

Method2(1.6,2.4,Int);

Writeln;

Writeln('|------------------------------------------------------------------|');

end;

end;

k:=k+1;

end;

Readln;

end.
