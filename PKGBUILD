# Maintainer: Brenton Horne <brentonhorne77@gmail.com>

pkgname=jupyterlab
pkgver=21254
_commit=729186781afcb0d6325e988289ed91bc08db7d60
pkgrel=1
pkgdesc="JupyterLab computational environment"
arch=(any)
url="https://github.com/jupyterlab/jupyterlab"
license=(custom)
makedepends=(python-setuptools nodejs python-recommonmark)
depends=(jupyterlab_server)
source=($pkgname-${_commit}.tar.gz::"https://github.com/jupyterlab/jupyterlab/archive/${_commit}.tar.gz"
jupyter-lab.desktop)
sha256sums=('cedd2a8e9fcd02395ce2a3592b2e2205ae70ff88a996a787cf891ca02d401c99'
            'd7ed2287b823a78b7fe05194180ad9b4602657d5e32b8ed548418039451c0434')

build() {
  cd $pkgname-${_commit}
  python setup.py build 
  cd docs
  make html
}

package() {
  cd $pkgname-${_commit}
  python setup.py install --skip-build --root="$pkgdir" --optimize=1

  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE

  # symlink to fix assets
  install -d "$pkgdir"/usr/share/jupyter
  ln -s `python -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())"`/jupyterlab "$pkgdir"/usr/share/jupyter/lab

  install -d "$pkgdir"/usr/share/{pixmaps,doc/${pkgname}}
  install -Dm644 examples/notebook/jupyter.png "$pkgdir"/usr/share/pixmaps/jupyter.png
  install -Dm755 $srcdir/jupyter-lab.desktop "$pkgdir"/usr/share/applications/jupyter-lab.desktop
  cp -r docs/build/html/* ${pkgdir}/usr/share/doc/${pkgname}
}
