import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class ConversorTemperaturaGUI extends JFrame {
    private JTextField txtValor;
    private JRadioButton rbCelsiusParaFahrenheit, rbFahrenheitParaCelsius;
    private JButton btnConverter;
    private JLabel lblResultado;

    public ConversorTemperaturaGUI() {
        setTitle("Conversor C° / F°");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout());

        JLabel lblValor = new JLabel("Valor:");
        txtValor = new JTextField(10);

        rbCelsiusParaFahrenheit = new JRadioButton("C° / F°");
        rbFahrenheitParaCelsius = new JRadioButton("F° / C°");
        ButtonGroup group = new ButtonGroup();
        group.add(rbCelsiusParaFahrenheit);
        group.add(rbFahrenheitParaCelsius);

        btnConverter = new JButton("Converter");
        lblResultado = new JLabel("Resultado: ");

        add(lblValor);
        add(txtValor);
        add(rbCelsiusParaFahrenheit);
        add(rbFahrenheitParaCelsius);
        add(btnConverter);
        add(lblResultado);

        btnConverter.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    double valor = Double.parseDouble(txtValor.getText());
                    double resultado;
                    String tipoClima;

                    if (rbCelsiusParaFahrenheit.isSelected()) {
                        resultado = (valor * 9 / 5) + 32;
                        lblResultado.setText("Resultado: " + resultado + " F°");
                    } else if (rbFahrenheitParaCelsius.isSelected()) {
                        resultado = (valor - 32) * 5 / 9;
                        lblResultado.setText("Resultado: " + resultado + " C°");
                    } else {
                        JOptionPane.showMessageDialog(null, "Selecione uma opção de conversão.");
                        return;
                    }
                    
                    // Definir tipo de clima e cor com base na temperatura em Fahrenheit
                    double tempFahrenheit = rbCelsiusParaFahrenheit.isSelected() ? resultado : valor;
                    
                    if (tempFahrenheit <= 64.4) {
                        tipoClima = "Frio";
                        lblResultado.setForeground(Color.BLUE);
                    } else if (tempFahrenheit >= 66.2 && tempFahrenheit <= 73.4) {
                        tipoClima = "Agradável";
                        lblResultado.setForeground(Color.GREEN);
                    } else if (tempFahrenheit >= 75.2 && tempFahrenheit <= 95) {
                        tipoClima = "Quente";
                        lblResultado.setForeground(Color.ORANGE);
                    } else {
                        tipoClima = "Muito Quente";
                        lblResultado.setForeground(Color.RED);
                    }
                    
                    lblResultado.setText(lblResultado.getText() + " - " + tipoClima);
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(null, "Por favor, insira um número válido.");
                }
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                ConversorTemperaturaGUI frame = new ConversorTemperaturaGUI();
                frame.setVisible(true);
            }
        });
    }
}
