# snowman
Для нарисования снеговика в Java, мы будем использовать классы JFrame и JPanel. Класс JFrame используется для создания окна приложения, а JPanel - для рисования графики.

Вот пример кода для нарисования снеговика:
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.Random;

public class Snowman extends JPanel implements ActionListener {
    private Timer timer;
    private int x, y;
    private int snowflakeSize = 10;

    public Snowman() {
        timer = new Timer(100, this);
        timer.start();
    }

    public void paintComponent(Graphics g) {
        super.paintComponent(g);
        drawSnowman(g, x, y);
    }

    private void drawSnowman(Graphics g, int x, int y) {
        g.setColor(Color.WHITE);
        g.fillOval(x, y, 100, 100);

        g.setColor(Color.ORANGE);
        g.fillOval(x + 30, y + 30, 40, 40);

        g.setColor(Color.BLACK);
        g.drawArc(x + 15, y + 15, 30, 30, 0, 180);
        g.drawArc(x + 55, y + 15, 30, 30, 0, 180);

        drawSnowflakes(g);
    }

    private void drawSnowflakes(Graphics g) {
        Random random = new Random();
        int x = random.nextInt((int) (getWidth() - snowflakeSize));
        int y = random.nextInt((int) (getHeight() - snowflakeSize));

        g.setColor(Color.WHITE);
        g.fillPolygon(new int[]{x, x - snowflakeSize, x + snowflakeSize}, new int[]{y, y - snowflakeSize, y + snowflakeSize}, 3);

        x = random.nextInt((int) (getWidth() - snowflakeSize));
        y = random.nextInt((int) (getHeight() - snowflakeSize));

        g.setColor(Color.WHITE);
        g.fillPolygon(new int[]{x, x - snowflakeSize, x + snowflakeSize}, new int[]{y, y - snowflakeSize, y + snowflakeSize}, 3);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        repaint();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                JFrame frame = new JFrame("Snowman");
                frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                frame.setContentPane(new Snowman());
                frame.setSize(400, 400);
                frame.setLocationRelativeTo(null);
                frame.setVisible(true);
            }
        });
    }
}
```
В этом примере мы создаем класс Snowman, наследующийся от JPanel. В методе paintComponent мы рисуем снеговика с двумя глазами и носом.

Мы также добавляем шестеренку Timer, которая вызывает метод actionPerformed каждые 100 миллисекунд. В этом методе мы вызываем метод repaint(), что приводит к перерисовке панели.

В методе drawSnowflakes мы генерируем случайные координаты для каждого снежинки и рисуем их в виде треугольника.
