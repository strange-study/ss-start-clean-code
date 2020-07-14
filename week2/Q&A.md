# Q & A

* pool.release(instance) 은 어떤가요?(전 별로 좋아 보이지 않아서... 질문을...)
* Q: [추상팩토리로 개선한 함수](#추상팩토리로-개선한-함수)에서 `EmployeFactory` 구현체를 `Employee` 상속 클래스마다 구현시키면 오버 엔지니어링일까?
  - ex. `CommisionedEmployeeFactory` -> `CommissionedEmployee`

  ```java
  public abstract class Employee {
    public abstract boolean isPayday();
    public abstract Money calculatePay();
    public abstract void deliverPay(Money pay);
  }

  public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
  }

  public class EmployeeFactoryImpl implements EmployeeFactory {
        public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
            switch (r.type) {
                // 이때 각 new 클래스 들은 위의 Employee abstract class를 상속받은 구현 클래스
                case COMMISSIONED:
                    return new CommissionedEmployee(r);
                case HOURLY:
                    return new HourlyEmployee(r);
                case SALARIED:
                    return new SalariedEmployee(r);
            default:
                throw new InvalidEmployeeType(r.type);
        }
    }
  }
  ```
* 부수효과를 일으키지마라! 에서 checkPasswordAndInitializeSession 은 함수가 한가지만 한다는 규칙을 위반한다는데, 이럴일이 은근 많은 것 같아서... 여러개 해도 된다는 건가.... ?
* if 문을 의미있는 이름의 함수로 뽑아내는 것에 대한 의견
  - 물론 ide로 찾아갈 수 있지만.. 실제 코드들에서는 이렇게 사용하는 경우가 많지 않았던 것 같음
* 같은 이야기를 중복하는 주석
  - 한국어 <-> 영어의 갭으로는 용인될 수?