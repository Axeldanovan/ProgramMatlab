Link YOUTUBE:https://youtu.be/UgU8G2sjtns

# ProgramMatlab


% UIWAIT makes AxelguiUTS wait for user response (see UIRESUME)
% uiwait(handles.figure1);
buat_axes = axes('unit', 'normalized', 'position', [0 0  1 1]);
backgroundnya = imread('yukina.jpg');
imagesc(backgroundnya);
set(buat_axes, 'handlevisibility', 'off', 'visible', 'off')



% --- Outputs from this function are returned to the command line.
function varargout = AxelguiUTS_OutputFcn(hObject, eventdata, handles) 
% varargout  cell array for returning output args (see VARARGOUT);
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Get default command line output from handles structure
varargout{1} = handles.output;


% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
[filename,pathname] = uigetfile('*.jpg;*.jpeg;*.png;*.tif');
 
try
    Img = imread(fullfile(pathname,filename));
    [~,~,m] = size(Img);
    if m == 3
        axes(handles.axes5)
        imshow(Img)
        handles.Img = Img;
        guidata(hObject, handles)
    end
catch
    msgbox('Please insert RGB Image')
end


% --- Executes on button press in pushbutton2.
function pushbutton2_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
popup1 = get(handles.popupmenu1,'value')
popup2 = get(handles.popupmenu2,'value')
popup3 = get(handles.popupmenu3,'value')

try
    if (popup1 == 1)                        %Normal
        if (popup2 == 1)                    %Histogram
            if (popup3 == 1)                %RGB
                Img = handles.Img;
                axes(handles.axes5)
                cla('reset')
                imshow(Img)

                R = Img(:,:,1);
                G = Img(:,:,2);
                B = Img(:,:,3);

                axes(handles.axes2)
                cla('reset')
                h = histogram(R(:),256);
                h.FaceColor = [1 0 0];
                h.EdgeColor = 'r';
                hold on

                h = histogram(G(:),256);
                h.FaceColor = [0 1 0];
                h.EdgeColor = 'g';

                h = histogram(B(:),256);
                h.FaceColor = [0 0 1];
                h.EdgeColor = 'b';
                grid on
                set(gca,'Xlim',[0 255])
                hold off
            elseif (popup3 == 2)            %Grayscale
                Img = handles.Img;
                Gray = rgb2gray(Img);

                axes(handles.axes5)
                cla('reset')
                imshow(Gray)

                axes(handles.axes2)
                cla('reset')
                h = histogram(Gray(:),256);
                h.FaceColor = [0.5 0.5 0.5];
                h.EdgeColor = [0.5 0.5 0.5];
                set(gca,'Xlim',[0 255])
                grid on

            else (popup3 == 3)              %Binary
                Gray = handles.Img;
                bw = im2bw(Gray,graythresh(Gray));

                axes(handles.axes5)
                cla('reset')
                imshow(bw)

                axes(handles.axes2)
                h = histogram(double(bw(:)),2);
                h.FaceColor = [0 0 0];
                h.EdgeColor = [0 0 0];
                set(gca,'Xlim',[0 1])
                grid on
            end
        else (popup2 == 2)                  
            if (popup3 == 1)                
                Img = handles.Img;
                axes(handles.axes1)
                cla('reset')
                imshow(Img)

                axes(handles.axes2)
                cla('reset')
                imhist(Img);

            elseif (popup3 == 2)            
                Img = handles.Img;
                Gray = rgb2gray(Img);

                axes(handles.axes1)
                cla('reset')
                imshow(Gray)

                axes(handles.axes2)
                cla('reset')
                imhist(Gray);

            else (popup3 == 3)              
                Gray = handles.Img;
                bw = im2bw(Gray,graythresh(Gray));

                axes(handles.axes2)
                cla('reset')
                imhist(bw);
            end
        end
    else (popup1 == 2)                      %Complement
        Img = handles.Img;
        Img_Comp = imcomplement(Img);
        if (popup2 == 1)                    
            if (popup3 == 1)                
                axes(handles.axes5)
                cla('reset')
                imshow(Img_Comp)

                R = Img_Comp(:,:,1);
                G = Img_Comp(:,:,2);
                B = Img_Comp(:,:,3);

                axes(handles.axes2)
                cla('reset')
                h = histogram(R(:),256);
                h.FaceColor = [1 0 0];
                h.EdgeColor = 'r';
                hold on

                h = histogram(G(:),256);
                h.FaceColor = [0 1 0];
                h.EdgeColor = 'g';

                h = histogram(B(:),256);
                h.FaceColor = [0 0 1];
                h.EdgeColor = 'b';
                set(gca,'Xlim',[0 255])
                grid on
                hold off
            elseif (popup3 == 2)            
                Gray_Comp = rgb2gray(Img_Comp);
                axes(handles.axes1)
                cla('reset')
                imshow(Gray_Comp)

                axes(handles.axes2)
                cla('reset')
                h = histogram(Gray_Comp(:),256);
                h.FaceColor = [0.5 0.5 0.5];
                h.EdgeColor = [0.5 0.5 0.5];
                set(gca,'Xlim',[0 255])
                grid on
            else (popup3 == 3)              
                Gray_Comp = handles.Img;
                bw_Comp = im2bw(Gray_Comp,graythresh(Gray_Comp));
                axes(handles.axes1)
                cla('reset')
                imshow(bw_Comp)

                axes(handles.axes2)
                h = histogram(double(bw_Comp(:)),2);
                h.FaceColor = [0 0 0];
                h.EdgeColor = [0 0 0];
                set(gca,'Xlim',[0 1])
                grid on
            end
        else (popup2 == 2)                  
            if (popup3 == 1)                
                axes(handles.axes5)
                cla('reset')
                imshow(Img_Comp)

                axes(handles.axes2)
                cla('reset')
                imhist(Img_Comp);

            elseif (popup3 == 2)            
                Gray_Comp = rgb2gray(Img_Comp);
                axes(handles.axes1)
                cla('reset')
                imshow(Gray_Comp)

                axes(handles.axes2)
                cla('reset')
                imhist(Gray_Comp);

            else (popup3 == 3)              
                Gray_Comp = handles.Img;
                bw_Comp = im2bw(Gray_Comp,graythresh(Gray_Comp));
                axes(handles.axes1)
                cla('reset')
                imshow(bw_Comp)

                axes(handles.axes2)
                cla('reset')
                imhist(bw_Comp);

            end
        end
    end
catch
    msgbox('Please insert RGB Image')
end
