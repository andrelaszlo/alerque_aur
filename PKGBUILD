# Maintainer: Florijan Hamzic <florijanh at gmail dot com>
_pypi_name='WeasyPrint'
pkgver=50
pkgrel=1
pkgdesc="Converts web documents (HTML, CSS, SVG, ...) to PDF."
license=('BSD')
arch=('any')
url="http://weasyprint.org/"
makedepends=('python' 'python-distribute')
depends=('python' 'pango>=1.29.3' 'gdk-pixbuf2>=2.25' 'cairo>=1.15.4'
         'python-cairo' 'python-cairosvg'
         'python-tinycss2' 'python-cssselect2>=0.1' 'python-html5lib'
         'python-cffi' 'python-cairocffi' 'python-pyphen' 'python-xcffib')

pkgname="python-weasyprint"
_pypi_name_inital=$(echo ${_pypi_name}|cut -c1)
source=("https://github.com/Kozea/WeasyPrint/archive/v${pkgver}.tar.gz")
md5sums=('f5fb5a6009f797abd171e8abf4626544')


package() {
  cd "$srcdir/WeasyPrint-$pkgver"
  python3 setup.py install --root="$pkgdir/" --optimize=1
}
