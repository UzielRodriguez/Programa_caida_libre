# Programa_caida_libre
function caidaLibre()
    % Solicitar al usuario qué desea calcular
    opcion = menu('Seleccione qué desea calcular:', 'Posición inicial', 'Velocidad inicial en y', 'Tiempo', 'Posición final', 'Velocidad final');
    
    % Solicitar los valores iniciales al usuario
    switch opcion
        case 1
            V0y = input('Ingrese la velocidad inicial en y (m/s): ');
            t = input('Ingrese el tiempo (s): ');
            a = 9.8; % Aceleración de la gravedad en el eje Y
            
            % Calcular y mostrar la posición inicial
            y0 = V0y * t + 0.5 * a * t^2;
            disp(['La posición inicial es: ' num2str(y0) ' m']);
            
        case 2
            t = input('Ingrese el tiempo (s): ');
            a = 9.8; % Aceleración de la gravedad en el eje Y
            Vf = input('Ingrese la velocidad final (m/s): ');
            
            % Calcular y mostrar la velocidad inicial en y
            V0y = Vf + a * t;
            disp(['La velocidad inicial en y es: ' num2str(V0y) ' m/s']);
            
        case 3
            V0y = input('Ingrese la velocidad inicial en y (m/s): ');
            a = -9.8; % Aceleración de la gravedad en el eje Y

            tf_option = menu('Seleccione qué desea utilizar para calcular el tiempo:', 'Posición final', 'Altura');
            
            if tf_option == 1
                yf = input('Ingrese la posición final (m): ');

                % Calcular el tiempo utilizando la fórmula de la chicharronera: t = (-V0y ± sqrt(V0y^2 + 2*a*yf)) / a
                discriminante = V0y^2 + 2*a*yf;

                if discriminante >= 0
                    t1 = (-V0y + sqrt(discriminante)) / a;
                    t2 = (-V0y - sqrt(discriminante)) / a;

                    disp(['El tiempo es: ' num2str(t1) ' s (positivo)']);
                    disp(['El tiempo es: ' num2str(t2) ' s (negativo)']);
                else
                    disp('No es posible calcular el tiempo. El discriminante es negativo.');
                end
            elseif tf_option == 2
                h = input('Ingrese la altura desde la cual caen las gotas de agua (m): ');

                % Calcular el tiempo utilizando la fórmula: t = sqrt((2 * h) / g)
                t = sqrt((2 * h) / abs(a));

                disp(['El tiempo es: ' num2str(t) ' s']);

                % Simulación de la caída libre
                t_sim = linspace(0, t, 100); % Rango de tiempo para la simulación
                pos_sim = -0.5 * a * t_sim.^2 + V0y * t_sim; % Posición en función del tiempo

                % Gráfica de posición en función del tiempo
                plot(t_sim, pos_sim, 'b');
                xlabel('Tiempo (s)');
                ylabel('Posición (m)');
                title('Simulación de caída libre');
                grid on;
                axis([0 t min(pos_sim) max(pos_sim)]);
                hold on;

                % Dibujar línea vertical en el tiempo t
                plot([t t], [min(pos_sim) max(pos_sim)], 'r--');
                legend('Posición vs. Tiempo', 'Tiempo calculado');
                hold off;
            else
                disp('Opción no válida.');
            end
            
        case 4
            y0 = input('Ingrese la posición inicial (m): ');
            V0y = input('Ingrese la velocidad inicial en y (m/s): ');
            t = input('Ingrese el tiempo (s): ');
            a = 9.8; % Aceleración de la gravedad en el eje Y
            
            % Calcular y mostrar la posición final
            posicion_final = y0 + V0y * t - 0.5 * a * t^2;
            disp(['La posición final es: ' num2str(posicion_final) ' m']);
            
        case 5
            t = input('Ingrese el tiempo (s): ');
            a = -9.8; % Aceleración de la gravedad en el eje Y
            
            V0y = input('Ingrese la velocidad inicial en y (m/s): ');
            
            % Calcular y mostrar la velocidad final
            Vf = V0y + a * t;
            disp(['La velocidad final es: ' num2str(Vf) ' m/s']);
            
            % Simulación de la caída libre
            t_sim = linspace(0, t, 100); % Rango de tiempo para la simulación
            pos_sim = V0y * t_sim + 0.5 * a * t_sim.^2; % Posición en función del tiempo

            % Gráfica de posición en función del tiempo
            plot(t_sim, pos_sim, 'b');
            xlabel('Tiempo (s)');
            ylabel('Posición (m)');
            title('Simulación de caída libre');
            grid on;
            axis([0 t min(pos_sim) max(pos_sim)]);
            hold on;

            % Dibujar línea vertical en el tiempo t
            plot([t t], [min(pos_sim) max(pos_sim)], 'r--');
            legend('Posición vs. Tiempo', 'Tiempo calculado');
            hold off;
            
        otherwise
            disp('Opción no válida.');
    end
end
