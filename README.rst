RITx: CYBER501x Cybersecurity Fundamentals - Personal study notes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This are my personal notes taken during the course `RITx: CYBER501x Cybersecurity Fundamentals <https://www.edx.org/course/cybersecurity-fundamentals>`_ at `edx.org <https://www.edx.org/>`_.

* `CYBER501x Cybersecurity Fundamentals notes <https://github.com/ricco386/CYBER501x-Cybersecurity-Fundamentals>`_
* `CYBER502x Computer Forensics notes <https://github.com/ricco386/CYBER502x-Computer-Forensics>`_

Feel free to use them during your study and if you find it useful you can star this repository. If you find a mistake or you think I have  missed something important I am more than happy to accept RP on this repo.

Notes are written in `Sphinx <https://www.sphinx-doc.org/en/master/>`_ documentation format. You can visit build notes at url: https://ricco386.github.io/CYBER501x-Cybersecurity-Fundamentals/

How to build the notes
======================

Create Python virtual environments and activate them::

	python3 -m venv envs3
	source envs3/bin/activate

Install the requiremetns::

	pip install -r requirements.txt

Build the Sphinx docs::

        make html

Run Python build-in webserver and open the build documentation in browser::

	cd docs/html
	python -m SimpleHTTPServer 8000
	firefox http://localhost:8000/


Richard von Kellner


