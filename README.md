SpringBoot + ES6 + React ��� ���Ϸ��÷���Ʈ �ҽ�
----
SpringBoot/ES6/React ������� ���߽� ��� �ҽ��� �ٷ� ����� �� �ִ� ���Ϸ��÷���Ʈ�Դϴ�.    
�ش� �ҽ����� ������ React ������ ���ԵǾ� �ֽ��ϴ�.

Specification
----
1. Backend
- SpringBoot 2.0.0.RELEASE (Spring MVC, Embedded Tomcat, Thymeleaf)

2. Frontend Builder
- Package manager : npm
- Bundler : webpack

3. ES6 Package ����
- babel
- react
- jquery
- bootstrap
- sass
- webpack-dev-server

Setup & Run
----
1. Git ��ġ �� �ҽ� �ٿ�ε�

Git ��ġ�ּ� : <https://git-scm.com/downloads>     

�ҽ� �ٿ�ε�     

```vim
$ git clone "https://github.com/jistol/boilerplate-boot-es6.git" boilerplate-boot-es6.git
```

2. npm ��ġ �� �ʱ�ȭ    
npm�� Node.js�� ��ġ�� ���� ��ġ �����մϴ�.

Node.js ��ġ�ּ� : <https://nodejs.org/en/>    

��ġ �� ROOT�������� �Ʒ� ��ɾ ���� �ʱ�ȭ�� �����մϴ�.    

```vim
$ npm install
``` 

�� ��ɾ �����ϸ� `node_modules` ������ ����鼭 `package.json`�� ���Ե� ���̺귯������ �ٿ�ε� �˴ϴ�.    

3. Backend ���� ����
Gradle ���带 ���� WAR������ �����Ͽ� ���� ���� �����ϳ� SpringBoot�� ���� �� �� �ִ� Gradle Task ������� �����Ͽ� ������ �⵿�� �� �ֽ��ϴ�.    
Gradle Wrapper�� �ҽ��� ���ԵǾ� �����Ƿ� ������ ��ġ �������� �Ʒ��� ���� ���� �����մϴ�.        

```vim
$ ./gradlew bootRun
```

������ �⺻������ 8080 ��Ʈ�� ���� �����մϴ�.    

4. ES6 �ҽ� ��ȯ �� Frontend Dev���� ����       
�Ϲ������� ES6�� �����ϴ� ���������� �����ϰų� babel�� ���� ȣȯ ������ �ҽ��� ���� �� ������ �� �ִµ�, �� �ҽ��� ������ ���̽��� �����ϵ��� ������ �ۼ��Ǿ� �ֽ��ϴ�.    
��ȯ�� �Ʒ��� ���� `package.json`�� npm ����� ���� ���� �� �� �ֵ��� ���ǵǾ� �ֽ��ϴ�.    

```javascript
...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "npm run build-js",
    "build-js": "./node_modules/.bin/webpack --config webpack.config.babel.js",
    "dev": "NODE_ENV='local' ./node_modules/.bin/webpack-dev-server"
  },
...
```    

��ȯ ������ �Ʒ��� ���� ���డ���մϴ�.    

```vim
$ npm run build
```

���� ���� ������ ���� ��������� �ٷ� �ݿ��ϱ� ���ؼ� `webpack-dev-server`�� ���� �� �� �ֽ��ϴ�.    
`webpack-dev-server`�� ���� ���Ǵ� `webpack.config.babel.js` ������ �Ʒ� �κп��� Ȯ�� �����ϸ� NODE_ENV ���� 'local' �� ��쿡�� �����ϵ��� �����Ǿ� �ֽ��ϴ�.     

```javascript
...
    if (process.env.NODE_ENV == 'local') {
        let url = `localhost`,
            protocol = `http`,
            devPort = 8090,
            proxyPort = 8080,
            demoEntry = {
            };

        config.entry = Object.assign({}, demoEntry, config.entry);

        config.devtool = 'inline-source-map';
        config.devServer = {
            inline: true,
            hot: true,
            historyApiFallback: true,
            host: url,
            port: devPort,
            proxy: {
                "!/dist/js/**": `${protocol}://${url}:${proxyPort}`,
                secure: false,
                changeOrigin: true,
            }
        };

        Object.keys(config.entry).forEach(key => {
            config.entry[key].push(`react-hot-loader/patch`);
            config.entry[key].push(`webpack-dev-server/client?${protocol}://${url}:${devPort}`);
            config.entry[key].push('webpack/hot/only-dev-server');
        });

        config.plugins.push(new webpack.HotModuleReplacementPlugin());
    }
...    
```

�Ʒ� ����� ���� ���� �� �� �ֽ��ϴ�.    

```vim
$ npm run dev
```

`webpack-dev-server`�� ����ϱ� ���ؼ��� 8090 ��Ʈ�� �����Ͽ��� �մϴ�.    

