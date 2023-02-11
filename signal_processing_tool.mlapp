classdef Alp_Doyduk_EE101_TermProject2 < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure            matlab.ui.Figure
        GridLayout          matlab.ui.container.GridLayout
        DesignedbyHasanAlpDoydukforEE101TermProject2Label  matlab.ui.control.Label
        LoadGraphButton     matlab.ui.control.Button
        RecordButton        matlab.ui.control.Button
        PlayButton          matlab.ui.control.Button
        DurationLabel       matlab.ui.control.Label
        Switch              matlab.ui.control.Switch
        DurationEditField   matlab.ui.control.EditField
        FastLabel           matlab.ui.control.Label
        HighLabel           matlab.ui.control.Label
        LowLabel            matlab.ui.control.Label
        SlowLabel           matlab.ui.control.Label
        SpeedKnob           matlab.ui.control.Knob
        SpeedKnobLabel      matlab.ui.control.Label
        AmplitudeKnob       matlab.ui.control.Knob
        AmplitudeKnobLabel  matlab.ui.control.Label
        UIAxes              matlab.ui.control.UIAxes
    end

    
    properties (Access = private)
        
        background_image = addpath("indir.png")
        n = 0
    end
    

    % Callbacks that handle component events
    methods (Access = private)

        % Button pushed function: RecordButton
        function RecordButtonPushed(app, event)
            
            audioObject = audiorecorder;

            duration = str2double(app.DurationEditField.Value);

            msgbox("Start Speaking");
            recordblocking(audioObject, duration);
            msgbox("End of Recording");
            
            %********************************************
            assignin("base", "audioObject", audioObject);
            %********************************************

        end

        % Button pushed function: PlayButton
        function PlayButtonPushed(app, event)
            
            try
                %*******************************************
                audioObject = evalin("base", "audioObject");
                %*******************************************
    
                if app.n == 0
                    y = getaudiodata(audioObject);
                    Fs = audioObject.SampleRate;
                
                    frequency_multiplier = app.SpeedKnob.Value;
                    amplitude_multiplier = app.AmplitudeKnob.Value;
                
                sound(y*amplitude_multiplier, Fs*frequency_multiplier);
    
                elseif app.n == 1
                    y = getaudiodata(audioObject);
                    Fs = audioObject.SampleRate;
    
                    frequency_multiplier = app.SpeedKnob.Value;
                    amplitude_multiplier = app.AmplitudeKnob.Value;
                    z = flipud(y);
    
                    sound(z*amplitude_multiplier, Fs*frequency_multiplier);
                end

            catch
                msgbox("Please record an audio")
            end
        end

        % Value changed function: Switch
        function SwitchValueChanged(app, event)
            
            value = app.Switch.Value;

            if app.Switch.Value == "Normal"
                app.n = 0;

            elseif app.Switch.Value == "Inverse"
                app.n = 1;

            end
        end

        % Button pushed function: LoadGraphButton
        function LoadGraphButtonPushed(app, event)
           
            try
                audioObject = evalin('base', 'audioObject');

                if app.n == 0
                    y = getaudiodata(audioObject);
                    Fs = audioObject.SampleRate;
                     
                    frequency_multiplier = app.SpeedKnob.Value;
                    amplitude_multiplier = app.AmplitudeKnob.Value;
        
                    t = 0:1/Fs*frequency_multiplier:(length(y)-1)/Fs*frequency_multiplier;
                    plot(app.UIAxes,[t],[y*amplitude_multiplier])
                  
                elseif app.n == 1
                    y = getaudiodata(audioObject);
                    Fs = audioObject.SampleRate;
                
                    multiplier = app.SpeedKnob.Value;
                    amplitude_multiplier = app.AmplitudeKnob.Value;

                    z = flipud(y);
               
                    t = 0:1/Fs*multiplier:(length(z)-1)/Fs*multiplier;
                    plot(app.UIAxes,[t],[z*amplitude_multiplier])
    
                end

            catch
                msgbox("Please record an audio")
            end
        end
    end

    % Component initialization
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure and hide until all components are created
            app.UIFigure = uifigure('Visible', 'off');
            app.UIFigure.Position = [100 100 722 598];
            app.UIFigure.Name = 'MATLAB App';

            % Create GridLayout
            app.GridLayout = uigridlayout(app.UIFigure);
            app.GridLayout.ColumnWidth = {'1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x'};
            app.GridLayout.RowHeight = {'1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x'};
            app.GridLayout.BackgroundColor = [1 0.8392 0.7098];

            % Create UIAxes
            app.UIAxes = uiaxes(app.GridLayout);
            title(app.UIAxes, 'Sound Graph')
            xlabel(app.UIAxes, 'Time')
            ylabel(app.UIAxes, 'Amplitude')
            zlabel(app.UIAxes, 'Z')
            app.UIAxes.XColor = [0 0 0];
            app.UIAxes.XTickLabel = {'0'; '0.2'; '0.4'; '0.6'; '0.8'; '1.0'; '1.2'; '1.4'; '1.6'; '1.8'; '2'};
            app.UIAxes.YColor = [0 0 0];
            app.UIAxes.ZColor = [0 0 0];
            app.UIAxes.FontSize = 14;
            app.UIAxes.Layout.Row = [1 6];
            app.UIAxes.Layout.Column = [1 14];

            % Create AmplitudeKnobLabel
            app.AmplitudeKnobLabel = uilabel(app.GridLayout);
            app.AmplitudeKnobLabel.HorizontalAlignment = 'center';
            app.AmplitudeKnobLabel.VerticalAlignment = 'top';
            app.AmplitudeKnobLabel.FontSize = 18;
            app.AmplitudeKnobLabel.Layout.Row = 11;
            app.AmplitudeKnobLabel.Layout.Column = [11 13];
            app.AmplitudeKnobLabel.Text = 'Amplitude';

            % Create AmplitudeKnob
            app.AmplitudeKnob = uiknob(app.GridLayout, 'continuous');
            app.AmplitudeKnob.Limits = [0 10];
            app.AmplitudeKnob.Layout.Row = [8 10];
            app.AmplitudeKnob.Layout.Column = [11 13];
            app.AmplitudeKnob.Value = 1;

            % Create SpeedKnobLabel
            app.SpeedKnobLabel = uilabel(app.GridLayout);
            app.SpeedKnobLabel.HorizontalAlignment = 'center';
            app.SpeedKnobLabel.VerticalAlignment = 'top';
            app.SpeedKnobLabel.FontSize = 18;
            app.SpeedKnobLabel.Layout.Row = 11;
            app.SpeedKnobLabel.Layout.Column = [2 4];
            app.SpeedKnobLabel.Text = 'Speed';

            % Create SpeedKnob
            app.SpeedKnob = uiknob(app.GridLayout, 'continuous');
            app.SpeedKnob.Limits = [0 2];
            app.SpeedKnob.Layout.Row = [8 10];
            app.SpeedKnob.Layout.Column = [2 4];
            app.SpeedKnob.Value = 1;

            % Create SlowLabel
            app.SlowLabel = uilabel(app.GridLayout);
            app.SlowLabel.HorizontalAlignment = 'center';
            app.SlowLabel.FontSize = 18;
            app.SlowLabel.Layout.Row = 10;
            app.SlowLabel.Layout.Column = 1;
            app.SlowLabel.Text = 'Slow';

            % Create LowLabel
            app.LowLabel = uilabel(app.GridLayout);
            app.LowLabel.HorizontalAlignment = 'center';
            app.LowLabel.FontSize = 18;
            app.LowLabel.Layout.Row = 10;
            app.LowLabel.Layout.Column = 10;
            app.LowLabel.Text = 'Low';

            % Create HighLabel
            app.HighLabel = uilabel(app.GridLayout);
            app.HighLabel.FontSize = 18;
            app.HighLabel.Layout.Row = 10;
            app.HighLabel.Layout.Column = 14;
            app.HighLabel.Text = 'High';

            % Create FastLabel
            app.FastLabel = uilabel(app.GridLayout);
            app.FastLabel.FontSize = 18;
            app.FastLabel.Layout.Row = 10;
            app.FastLabel.Layout.Column = 5;
            app.FastLabel.Text = 'Fast';

            % Create DurationEditField
            app.DurationEditField = uieditfield(app.GridLayout, 'text');
            app.DurationEditField.HorizontalAlignment = 'center';
            app.DurationEditField.FontSize = 18;
            app.DurationEditField.Layout.Row = 7;
            app.DurationEditField.Layout.Column = [3 4];
            app.DurationEditField.Value = '2';

            % Create Switch
            app.Switch = uiswitch(app.GridLayout, 'slider');
            app.Switch.Items = {'Normal', 'Inverse'};
            app.Switch.ValueChangedFcn = createCallbackFcn(app, @SwitchValueChanged, true);
            app.Switch.FontSize = 18;
            app.Switch.Layout.Row = 7;
            app.Switch.Layout.Column = [11 14];
            app.Switch.Value = 'Normal';

            % Create DurationLabel
            app.DurationLabel = uilabel(app.GridLayout);
            app.DurationLabel.HorizontalAlignment = 'right';
            app.DurationLabel.FontSize = 18;
            app.DurationLabel.Layout.Row = 7;
            app.DurationLabel.Layout.Column = [1 2];
            app.DurationLabel.Text = 'Duration';

            % Create PlayButton
            app.PlayButton = uibutton(app.GridLayout, 'push');
            app.PlayButton.ButtonPushedFcn = createCallbackFcn(app, @PlayButtonPushed, true);
            app.PlayButton.VerticalAlignment = 'top';
            app.PlayButton.BackgroundColor = [1 1 1];
            app.PlayButton.FontSize = 60;
            app.PlayButton.Layout.Row = [7 8];
            app.PlayButton.Layout.Column = [8 9];
            app.PlayButton.Text = '🔈';

            % Create RecordButton
            app.RecordButton = uibutton(app.GridLayout, 'push');
            app.RecordButton.ButtonPushedFcn = createCallbackFcn(app, @RecordButtonPushed, true);
            app.RecordButton.VerticalAlignment = 'top';
            app.RecordButton.BackgroundColor = [1 1 1];
            app.RecordButton.FontSize = 60;
            app.RecordButton.Layout.Row = [7 8];
            app.RecordButton.Layout.Column = [6 7];
            app.RecordButton.Text = '🎤';

            % Create LoadGraphButton
            app.LoadGraphButton = uibutton(app.GridLayout, 'push');
            app.LoadGraphButton.ButtonPushedFcn = createCallbackFcn(app, @LoadGraphButtonPushed, true);
            app.LoadGraphButton.BackgroundColor = [1 1 1];
            app.LoadGraphButton.FontSize = 60;
            app.LoadGraphButton.Layout.Row = [9 10];
            app.LoadGraphButton.Layout.Column = [7 8];
            app.LoadGraphButton.Text = '📈';

            % Create DesignedbyHasanAlpDoydukforEE101TermProject2Label
            app.DesignedbyHasanAlpDoydukforEE101TermProject2Label = uilabel(app.GridLayout);
            app.DesignedbyHasanAlpDoydukforEE101TermProject2Label.HorizontalAlignment = 'center';
            app.DesignedbyHasanAlpDoydukforEE101TermProject2Label.FontSize = 10;
            app.DesignedbyHasanAlpDoydukforEE101TermProject2Label.Layout.Row = 11;
            app.DesignedbyHasanAlpDoydukforEE101TermProject2Label.Layout.Column = [5 10];
            app.DesignedbyHasanAlpDoydukforEE101TermProject2Label.Text = 'Designed by Hasan Alp Doyduk for EE101 Term Project 2';

            % Show the figure after all components are created
            app.UIFigure.Visible = 'on';
        end
    end

    % App creation and deletion
    methods (Access = public)

        % Construct app
        function app = Alp_Doyduk_EE101_TermProject2

            % Create UIFigure and components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
end
