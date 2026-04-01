// Задание 1: Singleton + State 
enum SmartHomeProcessor {
    INSTANCE;
    AlarmSystem alarm = new AlarmSystem();
}

interface AlarmState {
    void handle(AlarmSystem ctx);
}

class DisarmedState implements AlarmState {
    public void handle(AlarmSystem ctx) {
        System.out.println("Сигнализация снята");
    }
}

class ArmedState implements AlarmState {
    public void handle(AlarmSystem ctx) {
        System.out.println("Тревога! Дверь открыта");
        ctx.setState(new AlarmStateImpl());
    }
}

class AlarmStateImpl implements AlarmState {
    public void handle(AlarmSystem ctx) {
        System.out.println("Сирена! Введите 9999");
    }
}

class AlarmSystem {
    private AlarmState state = new DisarmedState();
    void setState(AlarmState s) { state = s; }
    void trigger() { state.handle(this); }
}

// Задание 2: Observer
interface Observer { void update(String e); }
interface Subject {
    void attach(Observer o);
    void notify(String e);
}

class MotionSensor implements Subject {
    List<Observer> obs = new ArrayList<>();
    public void attach(Observer o) { obs.add(o); }
    public void notify(String e) { for (Observer o : obs) o.update(e); }
    void detect() { System.out.println("Движение!"); notify("движение"); }
}

class SecuritySystem implements Observer {
    public void update(String e) { System.out.println("Охрана: тревога!"); }
}

class MobileApp implements Observer {
    public void update(String e) { System.out.println("Push-уведомление"); }
}

// Задание 3: Strategy 
interface PaymentStrategy { void pay(double amount); }

class CreditCard implements PaymentStrategy {
    public void pay(double a) { System.out.println("Оплата картой: " + a); }
}
class PayPal implements PaymentStrategy {
    public void pay(double a) { System.out.println("Оплата PayPal: " + a); }
}
class Bitcoin implements PaymentStrategy {
    public void pay(double a) { System.out.println("Оплата Bitcoin: " + a); }
}

class ShoppingCart {
    double total = 1000;
    PaymentStrategy strategy;
    void setStrategy(PaymentStrategy s) { strategy = s; }
    void checkout() { strategy.pay(total); }
}

//  Задание 4: Комбинирование
class ExtendedAlarmSystem extends AlarmSystem implements Subject {
    List<Observer> observers = new ArrayList<>();
    public void attach(Observer o) { observers.add(o); }
    public void notify(String e) { for (Observer o : observers) o.update(e); }
    @Override
    void setState(AlarmState s) {
        super.setState(s);
        notify("Состояние изменено");
    }
}

// Демонстрация
public class Main {
    public static void main(String[] args) {
        // Задание 1
        SmartHomeProcessor p1 = SmartHomeProcessor.INSTANCE;
        SmartHomeProcessor p2 = SmartHomeProcessor.INSTANCE;
        System.out.println("Singleton: " + (p1 == p2));
        p1.alarm.trigger();
        p1.alarm.setState(new ArmedState());
        p1.alarm.trigger();

        // Задание 2
        MotionSensor ms = new MotionSensor();
        ms.attach(new SecuritySystem());
        ms.attach(new MobileApp());
        ms.detect();

        // Задание 3
        ShoppingCart cart = new ShoppingCart();
        cart.setStrategy(new CreditCard());
        cart.checkout();
        cart.setStrategy(new PayPal());
        cart.checkout();

        // Задание 4
        ExtendedAlarmSystem eAlarm = new ExtendedAlarmSystem();
        eAlarm.attach(new MobileApp()); // наблюдатель
        eAlarm.setState(new ArmedState());
        eAlarm.trigger();

        PaymentStrategy strategy = new CreditCard();
        strategy.pay(1500);
    }
}
