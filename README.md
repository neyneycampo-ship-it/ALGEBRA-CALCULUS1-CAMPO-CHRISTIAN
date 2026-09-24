
import math

# ---- ALGEBRA DEFINITIONS -----

def solve_linear(a, b, c):
    if a == 0:
        if b == c:
            return
        else:
            return
    x = (c - b) / a
    return f"Solution: x = {x}"

def solve_quadratic(a, b, c):
    if a == 0:
        return f"Not a quadratic equation (a=0). {solve_linear(b, c, 0)}"
   
    discriminant = (b ** 2) - (4 * a * c)
   
    if discriminant > 0:
        root1 = (-b + math.sqrt(discriminant)) / (2 * a)
        root2 = (-b - math.sqrt(discriminant)) / (2 * a)
        return f"Two real roots: x1 = {root1}, x2 = {root2}"
    elif discriminant == 0:
        root = -b / (2 * a)
        return f"One real root: x = {root}"
    else:
        real_part = -b / (2 * a)
        imag_part = math.sqrt(-discriminant) / (2 * a)
        return f"Complex roots: x1 = {real_part} + {imag_part}i, x2 = {real_part} - {imag_part}i"


# ---- CALCULUS 1 DEFINITIONS -----

def f(a, b, c, x):
    return a * (x ** 2) + b * x + c

def derivative_exact(a, b, x):
    return 2 * a * x + b

def derivative_numeric(a, b, c, x, h=1e-5):
    return (f(a, b, c, x + h) - f(a, b, c, x - h)) / (2 * h)

def estimate_limit(a, b, c, x0, h=1e-5):
    left_limit = f(a, b, c, x0 - h)
    right_limit = f(a, b, c, x0 + h)
    avg_limit = (left_limit + right_limit) / 2
    return f"Estimated limit as x -> {x0} is approx: {avg_limit:.6f}"

def integral_exact(a, b, c, x1, x2):
    def F(x):
        return (a / 3) * (x ** 3) + (b / 2) * (x ** 2) + c * x
    return F(x2) - F(x1)

def intergram_trapezoid(a, b, c, x1, x2, n=1000):
    h = (x2 - x1) / n
    total_sum = 0.5 * (f(a, b, c, x1) + f(a, b, c, x2))
   
    for i in range(1, n):
        total_sum += f(a, b, c, x1 + i * h)
       
    return total_sum * h


# ---- INPUT HELPER ------

def get_float(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Invalid input. Please enter a valid number.")


# ----- MAIN PROGRAM -----
def main():
    print("ALGEBRA & CALCULUS 1")
    print("FIND THE VALUE OF (X) = FORMULA: f(x)=(ax^2+bx+c) ")

    while True:
        print("\n1. Solve a linear equation (ax + b = c)")
        print("2. Solve a quadratic equation (ax^2 + bx + c = 0)")
        print("3. Evaluate f(x) = ax^2 + bx + c")
        print("4. Find the derivative f'(x) at a point)")
        print("5. Estimate a limit as x approaches a value")
        print("6. Compute a definite integral of f(x)")
        print("7. Quit")

        try:
            choice = int(input("\nEnter your choice: "))
        except ValueError:
            print("Invalid choice: Please choose 1-7. ")
            continue

        if choice == 1:
            a, b, c = get_float("a: "), get_float("b: "), get_float("c: ")
            print(solve_linear(a, b, c))

        elif choice == 2:
            a, b, c = get_float("a: "), get_float("b: "), get_float("c: ")
            print(solve_quadratic(a, b, c))

        elif choice == 3:
            a, b, c = get_float("a: "), get_float("b: "), get_float("c: ")
            x = get_float("x: ")
            print(f"f({x}) = {f(a, b, c, x)} ")

        elif choice == 4:
            a, b, c = get_float("a: "), get_float("b: "), get_float("c: ")
            x = get_float("x: ")
            exact = derivative_exact(a, b, x)
            numeric = derivative_numeric(a, b, c, x)
            print(f"exact f'({x}) = {exact} ")
            print(f"numeric f'({x}) = {numeric:.6f} (via central difference) ")

        elif choice == 5:
            a, b, c = get_float("a: "), get_float("b: "), get_float("c: ")
            x0 = get_float("x0(the value of x approaches): ")
            print(estimate_limit(a, b, c, x0))

        elif choice == 6:
            a, b, c = get_float("a: "), get_float("b: "), get_float("c: ")
            x1 = get_float("Lower bound x1: ")
            x2 = get_float("Upper bound x2: ")
            exact = integral_exact(a, b, c, x1, x2)
            numeric = intergram_trapezoid(a, b, c, x1, x2)
            print(f"Exact integral = {exact:.6f}")
            print(f"Numeric integral = {numeric:.6f} (via trapezoid rule, n = 1000)")

        elif choice == 7:
            print("Goodbye.")
            break

        else:
            print("Invalid choice: Please choose 1-7. ")

if __name__ == "__main__":
    main()
