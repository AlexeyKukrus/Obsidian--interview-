**Webpack** - это _сборщик статических модулей_ для современных приложений JavaScript
**bundle** - это результат, который мы получаем в процессе сборки
**Точка входа** указывает, какой модуль веб-пакет должен использовать, чтобы начать построение своего внутреннего графа зависимостей .
	Точек входа в приложение может быть несколько. Их можно указывать в формате ключ: значение, где ключ - название entry point-а
	entry - это путь к точке входа в приложение. Как правило это какой-то index.js файл. 
```javaScript
const path = require('path')
module.exports = {
	entry: path.resolve(__dirname, 'src', 'index.js'),
	//или
	entry: './src/file.js',
};

const path = require('path')
module.exports = {
	entry: {
		entry_name_1: path.resolve(__dirname, 'src', 'index_1.js'),
		entry_name_2: path.resolve(__dirname, 'src', 'index_2.js'),
	}
};
```
Output сообщает webpack куда отправлять создаваемые им _пакеты_ и как называть эти файлы. С названием файлов есть один нюанс - браузер кэширует при загрузке файлы и поэтому браузер всегда будет показывать кэшированную версию файла. Для того, чтобы этого избежать, можно воспользоваться способами нейминга файлов (1). После этого название файла будет обновляться и браузер будет читать свежий файл.
Также стоит автоматически чистить папку build, чтобы она не забивалась старыми файлами. При использовании clean: true (2) - перед сборкой папка build будет автоматически очищаться
output - указывается конфигурация того куда и как сборка будет сохраняться
```javaScript
const path = require('path')
module.exports = {
	entry: path.resolve(__dirname, 'src', 'index.js'),
	output: {
		path: path.resolve(__dirname, 'build'),
		filename: '[name].[contenthash].js', //1
		clean: true //2
	},
};
```

mode - выбор режима сборки - production и development. В development bundle не готов к проду, он не минимизируется. В production - bundle минимизирован - удалены все пробелы, переносы строк и комментарии.
```JSON
//package.json
 "scripts": {
    "build:dev": "webpack --env mode=development",
    "build:prod": "webpack --env mode=production"
  },
```
```javascript
//webpack.config.js
const path = require('path')
module.exports = (env) => {
	return {
		mode: env.mode ?? 'development',
		entry: path.resolve(__dirname, 'src', 'index.js'),
		output: {
			path: path.resolve(__dirname, 'build'),
			filename: '[name].[contenthash].js',
			clean: true
		}
	}
};
```
plugins - это дополнительные модули, которые расширяют функциональность компилятора Webpack и позволяют выполнять различные задачи во время сборки проекта. Плагины служат для настройки и оптимизации сборки, а также добавляют возможности и функциональность, которые невозможно достичь только с помощью загрузчиков.
В package.json плагины устанавливаются в dev-зависимости так как от них не зависит работа приложения после сборки, а в config.js файле под плагины есть отдельное свойство plugins и выглядит оно как массив экземпляров, вызванных с помощью оператора new.

```javascript
//webpack.config.js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = (env) => {
	return {
		mode: env.mode ?? 'development',
		entry: path.resolve(__dirname, 'src', 'index.js'),
		output: {
			path: path.resolve(__dirname, 'build'),
			filename: '[name].[contenthash].js',
			clean: true
		},
		plugins: [
			new HtmlWebpackPlugin({ template: path.resolve(__dirname, 'public', 'index.html')})
		],
	}
};
```