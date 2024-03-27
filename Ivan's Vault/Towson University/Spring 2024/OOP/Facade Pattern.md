---
tags:
  - COSC-436
  - spring2024
---

## Facade pattern

- The Facade pattern is used to provide a **simplified** interface to an otherwise complex system of classes, libraries, and frameworks. 
- Its purpose is to hide complexity and bloat of the system from the client and to offer an easy-to-use interface to interact with the system. 
- By using a facade, it helps in reducing dependencies on the internal workings of the system. 
- This makes it easier to use, understand, and maintain.
- Often used when a system is very complex or difficult to understand
	- involves a large number of interdependent classes or its source code is unavailable.
- **Does not** prevent the client from using the complex subsystem directly; rather, it provides a simpler way to access the functionality.

### Why It Is Used

1. **Simplify the Interface**: To provide a simple interface to a complex subsystem.
2. **Reduce Dependencies**: To decouple the subsystem from clients and other subsystems, thereby reducing the dependencies.
3. **Ease of Use and Maintenance**: To make the subsystem easier to use, understand, and maintain.
4. **Layering**: To introduce layers of abstraction which can help in structuring the system better.

## Examples

### CPU Example

```java
/* Complex parts */

class CPU {
    public void freeze() { ... }
    public void jump(long position) { ... }
    public void execute() { ... }
}

class Memory {
    public void load(long position, byte[] data) { ... }
}

class HardDrive {
    public byte[] read(long lba, int size) { ... }
}

/* Facade */

class ComputerFacade {
	private CPU processor;
	private Memory ram;
	private HardDrive hd;
	
	public ComputerFacade() {
		this.processor = new CPU();
		this.ram = new Memory();
		this.hd = new HardDrive();
	}
	
	public void start() {
		processor.freeze();
		ram.load(BOOT_ADDRESS, hd.read(BOOT_SECTOR, SECTOR_SIZE));
		processor.jump(BOOT_ADDRESS);
		processor.execute();
	}
}

/* Client */

class You {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.start();
    }
}
```

