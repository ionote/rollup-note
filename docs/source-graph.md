# Graph 的创建

## 实例化

## 生成模块图

调用 build 方法，启动模块图的构建。

```js
export default class Graph {
	implicitEntryModules = new Set();
	modulesById = new Map(); // 模块 map
	watchFiles = Object.create(null);

	constructor(options) {
		this.options = options;
		this.entryModules = null;
		// this.acornParser = acorn.Parser.extend([])
		this.moduleLoader = new ModuleLoader(this, this.modulesById);
	}

	async build() {
		await this.generateModuleGraph();
	}

	async generateModuleGraph() {
		({ entryModules: this.entryModules, implicitEntryModules: this.implicitEntryModules } =
			await this.moduleLoader.addEntryModules(normalizeEntryModules(this.options.input), true));
	}
}
```