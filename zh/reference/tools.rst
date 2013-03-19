Phalcon 开发工具
================
开发工具是生成脚手架代码的一系列脚本。使用简单的命令生成应用的核心代码，使得 Phalcon 开发过程更加容易。

.. highlights::
    **重要提醒:** Phalcon 框架 0.5.0 或以上版本需要使用本开发工具。强烈建议使用 PHP 5.3.6 或更高版本。如果你不需要命令行脚本而习惯网页工具，请参阅该`博客`_。

下载
----
可以从 Github_ 下载或克隆跨平台的开发工具包。

安装
^^^^
不同平台下开发工具的详细安装说明如下：

.. toctree::
   :maxdepth: 1

   wintools
   mactools
   linuxtools

显示可用的命令
--------------
输入 phalcon commands 可以显示一个可用的命令列表：

.. figure:: ../_static/img/tools-4.png
   :align: center

生成项目脚手架
--------------
使用 Phalcon 工具可以自动生成一个为 Phalcon 框架预先编写好的项目脚手架。默认情况下，项目脚手架生成器会使用 Apache mod_rewrite 模块。在 Web 服务器文档根目录下输入下列命令：

.. figure:: ../_static/img/tools-1.png
   :align: center

生成的项目目录结构如下：

.. figure:: ../_static/img/tools-2.png
   :align: center

使用 *--help* 命令参数查看命令帮助：

.. figure:: ../_static/img/tools-3.png
   :align: center

在浏览器中访问该项目显示如下：

.. figure:: ../_static/img/tools-6.png
   :align: center

生成控制器
----------
命令 "create-controller" 生成控制器脚手架。需要注意的是，必须在一个 Phalcon 项目目录下使用该命令。

.. figure:: ../_static/img/tools-5.png
   :align: center

脚本会生成下面的代码：

.. code-block:: php

    <?php

    class TestController extends Phalcon\Mvc\Controller
    {

        public function indexAction()
        {

        }

    }

数据库预配置
------------
开发工具生成项目时，也会自动创建 *app/config/config.ini* 配置文件。在使用开发工具生成模型和 CURD 增删改查脚手架前，必须更改数据库的设置以便正确连接到数据库。

更改 config.ini 文件的数据库部分:

.. code-block:: ini

    [database]
    adapter  = Mysql
    host     = "127.0.0.1"
    username = "root"
    password = "secret"
    name     = "store_db"

    [phalcon]
    controllersDir = "../app/controllers/"
    modelsDir      = "../app/models/"
    viewsDir       = "../app/views/"
    baseUri        = "/store/"

生成模型
--------
创建模型有好几种方法。可以从默认的数据库连接创建所有模型，也可以有选择性的创建。每一个表字段可以声明为模型的 public 属性，也可以使用 setters/getters 来操作。最简单的生成模型方法如下：

.. figure:: ../_static/img/tools-7.png
   :align: center

所有的表字段都被声明为可供直接访问的 public 属性。

.. code-block:: php

    <?php

    class Products extends \Phalcon\Mvc\Model
    {

        /**
         * @var integer
         */
        public $id;

        /**
         * @var integer
         */
        public $types_id;

        /**
         * @var string
         */
        public $name;

        /**
         * @var string
         */
        public $price;

        /**
         * @var integer
         */
        public $quantity;

        /**
         * @var string
         */
        public $status;

    }

使用 *--get-set* 参数可以将表字段声明为 protected，同时生成 public setter/getter 方法。在业务逻辑中使用相应的 setter/getter 方法。

.. code-block:: php

    <?php

    class Products extends \Phalcon\Mvc\Model
    {

        /**
         * @var integer
         */
        protected $id;

        /**
         * @var integer
         */
        protected $types_id;

        /**
         * @var string
         */
        protected $name;

        /**
         * @var string
         */
        protected $price;

        /**
         * @var integer
         */
        protected $quantity;

        /**
         * @var string
         */
        protected $status;


        /**
         * Method to set the value of field id
         * @param integer $id
         */
        public function setId($id)
        {
            $this->id = $id;
        }

        /**
         * Method to set the value of field types_id
         * @param integer $types_id
         */
        public function setTypesId($types_id)
        {
            $this->types_id = $types_id;
        }

        ...

        /**
         * Returns the value of field status
         * @return string
         */
        public function getStatus()
        {
            return $this->status;
        }

    }

模型生成器的好处在于开发者能使用生成器来控制变更。生成器增加或删除字段和属性，而不用担心忘记更改模型的内容。
详细的工作原理可以参阅下面的视频演示：

.. raw:: html

   <div align="center"><iframe src="http://player.vimeo.com/video/39213020" width="500" height="266" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe></div>

生成 CRUD 增删改查脚手架
------------------------
Scaffolding is a quick way to generate some of the major pieces of an application. If you want to create the models, views, and
controllers for a new resource in a single operation, scaffolding is the tool for the job.

Once the code is generated, it will have to be customized to meet your needs. Many developers avoid scaffolding entirely, opting
to write all or most of their source code from scratch. The generated code can serve as a guide to better understand of how the
framework works or develop prototypes. The screenshot below shows a scaffold based on the table "products":

.. figure:: ../_static/img/tools-9.png
   :align: center

The scaffold generator will build several files in your application, along with some folders. Here's a quick overview of what will be generated:

+----------------------------------------+--------------------------------+
| File                                   | Purpose                        |
+========================================+================================+
| app/controllers/ProductsController.php | The Products controller        |
+----------------------------------------+--------------------------------+
| app/models/Products.php                | The Products model             |
+----------------------------------------+--------------------------------+
| app/views/layout/products.phtml        | Controller layout for Products |
+----------------------------------------+--------------------------------+
| app/views/products/new.phtml           | View for the action "new"      |
+----------------------------------------+--------------------------------+
| app/views/products/edit.phtml          | View for the action "edit"     |
+----------------------------------------+--------------------------------+
| app/views/products/search.phtml        | View for the action "search"   |
+----------------------------------------+--------------------------------+
| app/views/products/edit.phtml          | View for the action "edit"     |
+----------------------------------------+--------------------------------+

When browsing the recently generated controller, you will see a search form and a link to create a new Product:

.. figure:: ../_static/img/tools-10.png
   :align: center

The "create page" allows you to create products applying validations on the Products model. Phalcon will automatically validate
not null fields producing warnings if any of them is required.

.. figure:: ../_static/img/tools-11.png
   :align: center

After performing a search, a pager component is available to show paged results. Use the "Edit" or "Delete" links in front of each result to perform such actions.

.. figure:: ../_static/img/tools-12.png
   :align: center

Web 界面工具
-------------
Also, if you prefer, it's possible to use Phalcon Developer Tools from a web interface. Check out the following screencast to figure out how it works:

.. raw:: html

   <div align="center"><iframe src="http://player.vimeo.com/video/42367665" width="500" height="266" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe></div>

PhpStorm IDE 内置工具
---------------------
The screencast below shows how to integrate developer tools with the `PhpStorm IDE`_. The configuration steps could be easily adapted to other IDEs for PHP.

.. raw:: html

   <div align="center"><iframe src="http://player.vimeo.com/video/43455647" width="500" height="266" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe></div>

结论
-----
Phalcon 开发工具提供简单的方式生成应用代码，减少开发时间并降低潜在的编码错误风险。

.. _博客: http://blog.phalconphp.com/post/23251010409/dont-like-command-line-and-consoles-no-problem
.. _Github: https://github.com/phalcon/phalcon-devtools
.. _Bootstrap: http://twitter.github.com/bootstrap/
.. _PhpStorm IDE: http://www.jetbrains.com/phpstorm/