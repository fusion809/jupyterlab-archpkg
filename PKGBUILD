# Maintainer: Brenton Horne <brentonhorne77@gmail.com>

pkgname=jupyterlab
pkgver=16280
_commit=ee4dae8dffc8d7ce393502971b804dcd4290e2a6
pkgrel=1
pkgdesc="JupyterLab computational environment"
arch=(any)
url="https://github.com/jupyterlab/jupyterlab"
license=(custom)
makedepends=(python-setuptools nodejs python-recommonmark)
depends=(jupyterlab_server)
source=($pkgname-${_commit}.tar.gz::"https://github.com/jupyterlab/jupyterlab/archive/${_commit}.tar.gz"
jupyter-lab.desktop)
sha256sums=('8a211afdaff2d7a98fecb186b3158d7e345c42d7852d60d4fa48e8d3247fb8f0'
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
