# PDE-Transformer: A Continuous Dynamical Systems Approach to Sequence Modeling

[![arXiv](https://img.shields.io/badge/arXiv-2510.03272-b31b1b.svg)](https://arxiv.org/abs/2510.03272)
[![GitHub](https://img.shields.io/badge/GitHub-Code-blue.svg)](https://github.com/XueqingZhou/PDE-Transformer)

Official implementation of **PDE-Transformer**, a novel sequence modeling paradigm that casts the forward pass of a Transformer as the numerical discretization of a continuous reaction-diffusion system.

## Overview

PDE-Transformer introduces a continuous dynamical systems approach to sequence modeling by:

- Modeling token embeddings as solutions to a partial differential equation (PDE)
- Designing an **Adaptive PDE Diffusion Layer** with linear time complexity
- Providing principled guidelines for integrating PDE layers in Transformers
- Achieving 4.1 pp average accuracy gain on Long Range Arena benchmark

## Links

- **Paper**: [arXiv:2510.03272](https://arxiv.org/abs/2510.03272)
- **PDF**: [Download PDF](https://arxiv.org/pdf/2510.03272)
- **Code**: [GitHub Repository](https://github.com/XueqingZhou/PDE-Transformer)

## Citation

```bibtex
@article{zhang2025pde,
  title={PDE-Transformer: A Continuous Dynamical Systems Approach to Sequence Modeling},
  author={Zhang, Yukun and Zhou, Xueqing},
  journal={arXiv preprint arXiv:2510.03272},
  year={2025},
  url={https://arxiv.org/abs/2510.03272}
}
```

## Authors

- **Yukun Zhang**<sup>*</sup> - The Chinese University of Hong Kong
- **Xueqing Zhou**<sup>*</sup> - Fudan University

<sup>*</sup>Equal contribution

## License

This project is licensed under the terms specified in the repository.

## Acknowledgments

This template was borrowed from [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template) which was adopted from the [Nerfies](https://nerfies.github.io) project page under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
