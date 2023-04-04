# **Writeup - VishwaCTF**

* Category **reverse** 
* Name **Wednesday Thursday Friday** 
* Difficulty **Medium**


## Description
Enter the Flag !!

## **Solution**
Apparently it's a program rhat runs some checks on the input and tells you if it's a valid flag, first step is to understand how it checks the flag, so i open it with ghidra.  
Turns out that it wants 34 characters in the first argument, it interprets them as integers and in the main function there's a system of equations that, if solved, would give values describing the correct flag.

It would be very time consuming to solve by hand, but luckily some automatic tools exist, such as angr.

So i used angr in a python script to get the correct input to make the program execute successfully.

script used:
```python
import angr
import claripy

def main():
    
    binary_path = './solveme'
    project = angr.Project(binary_path, auto_load_libs=False, main_opts={'base_addr' : 0x00100000})

    input_length = 34
    flag_chars = [claripy.BVS(f'flag_{i}', 8) for i in range(input_length)]
    flag = claripy.Concat(*flag_chars + [claripy.BVV(b'\x00')])  

    
    state = project.factory.entry_state(args=[binary_path, flag])
    for k in flag_chars:
        state.solver.add(k >= 0x20)  
        state.solver.add(k <= 0x7e)

    
    simgr = project.factory.simulation_manager(state)

    
    def correct(state):
        try:
            return b'CORRECT :)' in state.posix.dumps(1)
        except:
            return False

    def wrong(state):
        try:
            return b"INCORRECT :(" in state.posix.dumps(1)
        except:
            return False

   
    simgr.explore(find=correct, avoid=wrong)

    
    if simgr.found:
        found_state = simgr.found[0]
        solution = found_state.solver.eval(flag, cast_to=bytes).decode(errors='ignore')
        return solution.rstrip('\x00')
    else:
        return "No solution found"

if __name__ == '__main__':
    solution = main()
    print(f"Correct input string: {solution}")
```

flag: VishwaCTF{N3V3r_60NN4_61V3_Y0U_UP}