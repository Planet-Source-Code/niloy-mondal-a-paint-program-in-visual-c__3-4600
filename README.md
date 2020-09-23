<div align="center">

## ^A Paint Program in Visual C\+\+^


</div>

### Description

This shows how to make a simple free-hand drawing program in Visual C++. The code is commented.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Niloy Mondal](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/niloy-mondal.md)
**Level**          |Beginner
**User Rating**    |4.2 (54 globes from 13 users)
**Compatibility**  |Microsoft Visual C\+\+
**Category**       |[Graphics/ Sound](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics-sound__3-15.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/niloy-mondal-a-paint-program-in-visual-c__3-4600/archive/master.zip)

### API Declarations

```
#include<windows.h>
```


### Source Code

```
//Programmer:- Niloy Mondal. Email:- niloygk@yahoo.com
#include <windows.h>
LRESULT CALLBACK WndProc (HWND, UINT, WPARAM, LPARAM) ;
int lastx,lasty,x,y;		//GLOBAL VARIABLES used in drawing.
//The WinMain contains all formality stuff that must be written in almost every Windows Program.
int WINAPI WinMain (HINSTANCE hInstance, HINSTANCE hPrevInstance,
     PSTR szCmdLine, int iCmdShow)
{
  static TCHAR szAppName[] = TEXT ("Paint") ;//Winddow Class name
  HWND   hwnd ;
  MSG   msg ;
  WNDCLASS  wndclass ;
  wndclass.style   = CS_HREDRAW | CS_VREDRAW ;
  wndclass.lpfnWndProc = WndProc ;
  wndclass.cbClsExtra = 0 ;
  wndclass.cbWndExtra = 0 ;
  wndclass.hInstance  = hInstance ;
  wndclass.hIcon   = LoadIcon (NULL, IDI_APPLICATION) ;
  wndclass.hCursor  = LoadCursor (NULL, IDC_ARROW) ;
  wndclass.hbrBackground = (HBRUSH) GetStockObject (WHITE_BRUSH) ;
  wndclass.lpszMenuName = NULL ;
  wndclass.lpszClassName = szAppName ;
  if (!RegisterClass (&wndclass))
  {
   MessageBox (NULL, TEXT ("This program requires Windows 98!"),
      szAppName, MB_ICONERROR) ;
   return 0 ;
  }
  hwnd = CreateWindow (szAppName,     // window class name
       TEXT ("Paint in Visual C++."), // window caption
       WS_OVERLAPPEDWINDOW,  // window style
       CW_USEDEFAULT,    // initial x position
       CW_USEDEFAULT,    // initial y position
       CW_USEDEFAULT,    // initial x size
       CW_USEDEFAULT,    // initial y size
       NULL,      // parent window handle
       NULL,      // window menu handle
       hInstance,     // program instance handle
       NULL) ;      // creation parameters
  ShowWindow (hwnd, iCmdShow) ;
  UpdateWindow (hwnd) ;
  while (GetMessage (&msg, NULL, 0, 0))				//The Message Loop
  {
   TranslateMessage (&msg) ;
   DispatchMessage (&msg) ;
  }
  return msg.wParam ;
}
void line(HDC _hdc,int x1,int y1,int x2,int y2)//This function draws line by the given four coordinates.
{
	MoveToEx(_hdc,x1,y1,NULL);
	LineTo(_hdc,x2,y2);
}
LRESULT CALLBACK WndProc (HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam)
{
  HDC   hdc ;
  PAINTSTRUCT ps ;
  RECT  rect ;
  switch (message)
  {
	 case WM_LBUTTONDOWN:					//If Left mouse button is pressed
			lastx=LOWORD(lParam);			//Store the x-coordiante in lastx
			lasty=HIWORD(lParam);			//Store the y-coordinate in lasty
			return 0;
  case WM_MOUSEMOVE:						//When mouse is moved on the client area (or form for VB users)
		 hdc = GetDC(hwnd);					//hdc is handle to device context
		 x=LOWORD(lParam);					//Store the current x
		 y=HIWORD(lParam);					//Store the current y
		 if (wParam & MK_LBUTTON)			//If Left mouse button is down then draw
		 {
			line(hdc,lastx,lasty,x,y);		//Draw the line frome the last pair of coordiates to current
			lastx=x;						//The current x becomes the lastx for next line to be drawn
			lasty=y;						//The current y becomes the lasty for next line to be drawn
		 }
		 ReleaseDC(hwnd,hdc);
		 return 0;
  case WM_PAINT:
   hdc = BeginPaint (hwnd, &ps) ;
   GetClientRect (hwnd, &rect) ;
		 TextOut(hdc,0,0 ,"Programmer :- Niloy Mondal. Email:- niloygk@yahoo.com",53);
		 EndPaint (hwnd, &ps) ;
   return 0 ;
  case WM_DESTROY:
   PostQuitMessage (0) ;
   return 0 ;
  }
  return DefWindowProc (hwnd, message, wParam, lParam) ;
}
```

